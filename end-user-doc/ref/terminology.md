This document explains about the terms used in the Handbook.

[A](#a) | [B](#b) | [D](#d) | [F](#f) | [H](#h) | [I](#i) | [Q](#q) | [T](#t) | [V](#v)

---


## A

### alias

An alias is a virtual index name that can point to one or more indices.

### aggregation

Aggregations let you tap into OpenSearch’s powerful analytics engine to analyze
your data and extract statistics from it.

Note: OpenSearch doesn’t support aggregations on a `text` field.

### aggregation type

There are three main types of aggregations:

  - Metric aggregations - Calculate metrics such as sum, min, max, and avg on
    numeric fields.
  - Bucket aggregations - Sort query results into groups based on some criteria.
  - Pipeline aggregations - Pipe the output of one aggregation as an input to
    another.


## B

### bucket

A set of documents in BAP that have certain characteristics in common. For
example, matching documents might be bucketed by name, type, or date range.


## D

### dashboard

A collection of visualizations that provide insights into your data.

### data source

The data sources are the platforms and tools from where BAP can pull data to
analyze.

### document

A JSON object containing data stored and indexed in OpenSearch.


## F

### field

A key-value pair in a document.


## H

### HatStall

HatStall is a deprecated web interface for [SortingHat](#sortinghat) databases.

## I

### index(es)/indices

A collection of JSON documents.

### index pattern

A string containing a wildcard (*) pattern that can match multiple indices or
aliases.

### ingestion

The process of collecting data from various data sources and sending it to
OpenSearch.


## Q

### query

Request for information about your data. You can think of a query as a question,
written in a way OpenSearch understands.

## S
### SortingHat

SortingHat is the identity management subsystem of Bitergia Analytics Platform.
It is available in `https://[INSTANCE].biterg.io/identities`.
See more about affiliations [here](../advanced/affiliations/).

## T

### text

Unstructured content, such as a product description or log message which can be
used for better analysis.


## V

### visualization

A graphical representation of query results in BAP's web user interface.
