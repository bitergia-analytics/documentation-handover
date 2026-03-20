# Stack Overflow

Stack Exchange is a network of question-and-answer (Q&A) websites on topics in
diverse fields, each site covering a specific topic, where questions, answers,
and users are subject to a reputation award process.

Stack Overflow, which is a question and answer site for professional and
enthusiast programmers, is a part of the Stack Exchange network of Q&A sites. It
is the most popular Q&A site on the network. Each site uses the same software
but is generally geared towards certain topics. You can find the list of [all
the sites of Stack Exchange](https://stackexchange.com/sites).


## Data from Stack Exchange

### Questions and Answers

The documents in this index are either about questions or answers to those
questions. For both, BAP has information about the author, as well as up-votes
and down-votes. For answers, BAP tracks what question they belong to and which
was designated as "accepted answer". BAP can analyze the tags associated to the
questions.


## Data Model

The information for this data set is provided through indices in ElasticSearch.
Those are used to calculate the metrics and charts in the dashboard. In case you
need information about them it is available below.

| Index Pattern | Content |
| --- | --- |
| [stackoverflow](../ref/datamodel/stackoverflow.md) | Questions and answers are stored in the index, so a document can be either an answer or a question |
