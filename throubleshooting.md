# Throubleshooting

- [Mordred](#mordred)
    - [Unhealthy mordred container](#unhealthy-mordred-container)
    - [The index is not updated](#the-index-is-not-updated)
    - [Pontoon session id expired](#pontoon-session-id-expired)
        - [Obtaining the Session ID](#obtaining-the-session-id)
        - [Using the Session ID](#using-the-session-id)
    - [Bugzillarest error](#bugzillarest-error)
        - [Error in logs](#error-in-logs)
        - [Workaround](#workaround)

## Mordred

### Unhealthy mordred container

If the mordred container is unhealthy, you can check the logs to find out the
issue at `/docker/mordred/instances/test/logs/all.log`.

```bash
root@all-in-one-0:~# docker ps

CONTAINER ID   IMAGE                                COMMAND                  CREATED       STATUS                    PORTS     NAMES
969a90b912a1   bitergia/bitergia-analytics:0.37.0   "/bin/sh -c ${DEPLOY…"   3 weeks ago   Up 22 hours (unhealthy)             mordred_test
```

When the mordred container is unhealthy, is because the Task Manager is not
able to connect to OpenSearch, and the thread will be stop, in this case the
`github2:issue` and `git` threads.

```bash
root@bitergio-mordred-1:/docker/mordred/instances/sta/logs# cat all.log | grep ERROR | grep "Task Manager"

2026-03-09 15:30:30,394 - Test - sirmordred.task_manager - ERROR - [github2:issue] Exception in Task Manager 500 Server Error: Internal Server Error for url: https://bap-opensearch-manager-0:9200/bap_test_github2-issue_260122_enriched_260122/_update_by_query?wait_for_completion=true&conflicts=proceed

2026-03-09 15:30:37,333 - Test - sirmordred.task_manager - ERROR - [git] Exception in Task Manager TransportError(500, 'search_phase_execution_exception', 'node [cv1rlvDRSd6SwWdm8vPJrx] is not available')
```

To solve this issue, you can restart the mordred container.

1. On the `control-node`
   1. stop the mordred container

      ```bash
      ansible-playbook -i environments/<project>/inventory playbook/stop_mordred.yml
      ```

1. On the `all-in-one-0` or `mordred-0` node depends on your infrastructure:
   1. Change to sudo `sudo su`
   1. Start the mordred container

      ```bash
      docker start mordred_test
      ```

### The index is not updated

If the index is not updated, you can check the logs to find out the issue at
`/docker/mordred/instances/test/logs/all.log`.

- For example, if you want to see the logs of the `git` thread, you can filter
 the logs with `grep`:

```bash
root@all-in-one-0:~# cd /docker/mordred/instances/test/logs
root@all-in-one-0:/docker/mordred/instances/test/logs# cat all.log | grep -v autorefresh | grep git] | tail
```

Maybe you don't have permissions to clone the repository or it does not exist.

### Pontoon session id expired

Pontoon does not provide API tokens or personal access tokens. Authentication must be performed using the Django session cookie (`sessionid`) generated after logging into the web interface.

The `sessionid` cookie remains valid for 14 days. After expiration, the login process must be repeated and a new session ID retrieved.

#### Obtaining the Session ID

- Log in (or create an account) at https://pontoon.mozilla.org/
- Open your browser’s Developer Tools (F12).
- Retrieve the `sessionid` cookie:
  - Application/Storage > Cookies > pontoon.mozilla.org > sessionid

#### Using the Session ID

- Open the `setup.cfg` file
- Update the field `session-id` under `[pontoon]` section:
  ```
  [pontoon]
  ...
  session-id = <your-session-id>
  ```

### Bugzillarest error

During data collection from BugzillaREST, the API may occasionally return internal errors that interrupt the collection process.

These failures are temporary but may persist for hours, days, or even weeks before the endpoint becomes usable again.

#### Error in logs

The failure usually appears in the logs as:

```
2025-09-08 09:28:21,511 - Project - grimoire_elk.elk - ERROR - Error feeding raw from bugzillarest (https://bugzilla.mozilla.org): 400 Client Error: Bad Request for url: https://bugzilla.mozilla.org/rest/bug?last_change_time=2025-09-02T17%3A53%3A02Z&limit=1&order=changeddate&include_fields=_all&offset=1
```

This typically indicates that one or more items returned by the API cannot be processed correctly.

#### Workaround

The workaround is to skip the problematic item(s) and resume the collection from a later timestamp.

1. Identify the timestamp where the failure occurs from the logs.

2. Test the endpoint using Perceval, starting from that timestamp and retrieving a single bug:

```
perceval bugzillarest https://bugzilla.mozilla.org \
  --max-bugs 1 \
  --from-date 2025-09-24T06:47:16+00:00 \
  --no-archive \
  -t <token>
```

3. Increment the `last_change_time` value until the request succeeds. Try to adjust the timestamp at the minute level to identify the first valid item and minimize the number of skipped items.

4. Update the `from-date` parameter in `setup.cfg` to the working timestamp:
   ```
   [bugzillarest]
   ...
   from-date = YYYY-MM-DDTHH:MM:SS+00:00
   ```
5. Restart the collection process.
