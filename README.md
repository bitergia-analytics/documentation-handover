# Bitergia Analytics Documentation Handover

Welcome to the documentation for Bitergia Analytics Platform (BAP). This repository contains essential guides for operating, configuring, and troubleshooting the BAP infrastructure.

## Platform Overview

The Bitergia Analytics Platform (BAP) is a software development analytics solution built on [GrimoireLab](https://chaoss.github.io/grimoirelab/). It provides organizations with powerful insights into their development processes through data collection, enrichment, and visualization.

**Core Architecture:**
- **Data Collection Layer**: Perceval collects raw data from various sources (Git, GitHub, GitLab, Jira, etc.)
- **Data Processing**: GrimoireELK enriches and transforms raw data into analyzable metrics
- **Storage**: OpenSearch stores both raw and enriched data with configurable retention policies
- **Identity Management**: SortingHat unifies contributor identities across multiple platforms
- **Orchestration**: Mordred coordinates the entire data pipeline
- **Visualization**: OpenSearch Dashboards presents interactive analytics and reports

**Deployment Model:**
The platform runs on cloud infrastructure (GCP, AWS) with Infrastructure as Code (OpenTofu) and configuration management (Ansible), enabling reproducible and scalable deployments across different environments.

For a complete architectural overview, see [BAP Architecture Documentation](https://github.com/bitergia-analytics/bap-deployment-toolkit/blob/main/docs/architecture_overview.md)

## 📚 Documentation Index

### 🚀 [Operation Guide](operation.md)
Complete infrastructure management guide for the Bitergia Analytics Platform.

- [Control Node](operation.md#control-node) - Infrastructure management overview
- [Upgrading BAP Versions](operation.md#upgrading-bap-versions) - Platform version management
- [Mordred Operations](operation.md#mordred-operations) - Container management and configuration
- [Source synchronization](operation.md#source-synchronization) - Sources synchronization

### ⚙️ [Mordred Configuration](mordred_configuration.md)
Detailed guide for configuring GrimoireLab data collection and analysis.

- [Configuration File](mordred_configuration.md#configuration-file) - Setting up `setup.cfg` for data sources
- [Projects File](mordred_configuration.md#projects-file) - Configuring `projects.json` for repository analysis
- [Data Source Examples](mordred_configuration.md#data-source-examples)
  - [Git](mordred_configuration.md#git) - Git repository analysis configuration
  - [GitHub](mordred_configuration.md#github) - GitHub issues, pulls, and repository data collection

### 🔍 [OpenSearch Configuration](opensearch_configuration.md)
Configuration guide for OpenSearch role-based access control, data privacy, and indices management.

- [Pseudoanonymization](opensearch_configuration.md#pseudoanonymization) - Role-based data privacy and field masking configuration
- [Custom indices](opensearch_configuration.md#custom-indices) - Managing tenant-specific custom indices

### 👤 [User Management](user_management.md)
Step-by-step instructions for managing users and permissions across the platform.

- [SortingHat](user_management.md#sortinghat)
  - [Add User](user_management.md#add-user) - Creating new platform users
  - [Add Admin User](user_management.md#add-admin-user) - Creating administrative users
  - [Remove User](user_management.md#remove-user) - User deletion procedures
  - [Change Permissions](user_management.md#change-permissions) - Role and permission management
- [OpenSearch](user_management.md#opensearch)
  - [Roles](user_management.md#opensearch-roles)
  - [Add User](user_management.md#add-user-1) - OpenSearch user creation
  - [Change Password](user_management.md#change-password) - Password management
  - [Delete User](user_management.md#delete-user) - User removal in OpenSearch

### 📖 [End-User Documentation](end-user-doc/README.md)
Guides and tutorials for end users working with SortingHat and OpenSearch.

- [New to Bitergia Analytics Platform?](end-user-doc/README.md#new-to-bitergia-analytics-platform) - Getting started guides and tutorials
- [Supported Data Sets](end-user-doc/README.md#supported-data-sets) - Integration guides for all data sources  
- [Advanced Instructions](end-user-doc/README.md#advanced-instructions) - Power user features and API documentation
- [Reference](end-user-doc/README.md#reference) - Data models, terminology, and technical references

### 🔧 [Troubleshooting Guide](troubleshooting.md)
Solutions for common issues and error scenarios in the BAP environment.

- [Mordred](troubleshooting.md#mordred)
  - [Unhealthy Mordred Container](troubleshooting.md#unhealthy-mordred-container) - Diagnosing and fixing container health issues
  - [Missing or Outdated Data](troubleshooting.md#missing-or-outdated-data) - Troubleshooting data collection and update problems
  - [Pontoon Session ID Expired](troubleshooting.md#pontoon-session-id-expired) - Handling authentication issues with Mozilla Pontoon
    - [Obtaining the Session ID](troubleshooting.md#obtaining-the-session-id)
    - [Using the Session ID](troubleshooting.md#using-the-session-id)
  - [Bugzillarest Error](troubleshooting.md#bugzillarest-error) - Resolving BugzillaREST API collection failures
    - [Error in Logs](troubleshooting.md#error-in-logs)
    - [Workaround](troubleshooting.md#workaround)
- [End user FAQ](end-user-doc/new/faq.md)
  - [Identities](end-user-doc/new/faq.md#identities) - Questions about identity and affiliation management
  - [Data Sources Management](end-user-doc/new/faq.md#data-sources-management) - Common questions about adding repositories and data sources
  - [Dashboards](end-user-doc/new/faq.md#dashboards) - Troubleshooting visualizations and dashboard problems
  - [Metrics](end-user-doc/new/faq.md#metrics) - Understanding and interpreting metrics data

## 🔗 External Resources

- [BAP Deployment Toolkit](https://github.com/bitergia-analytics/bap-deployment-toolkit) - Official deployment repository
- [SirMordred Backends](https://github.com/chaoss/grimoirelab-sirmordred) - GrimoireLab orchestrator documentation
- [Bitergia Backends](https://github.com/bitergia-analytics/bitergia-analytics-elk-backends) - Custom data source backends
- [OpenSearch](https://docs.opensearch.org/) - Official OpenSearch documentation
