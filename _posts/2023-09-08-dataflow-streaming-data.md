---
title: Group Streaming Data by Key in Dataflow
date: 2023-09-08 18:22:00 +1000
categories: [GCP, PoC]
tags: [dataflow, gcp, java]
pin: false
math: false
mermaid: false
image:
  path: /mac.jpg
  alt: 'Photo by Pixabay: https://www.pexels.com/photo/macbook-pro-459653/'
---

Dataflow is a managed service for Apache Beam on GCP. It can apply the same data transformation on both batch and streaming data. Apache Beam implements the map-reduce model where each data element can be processed individually on multiple workers then group and aggregate to get desired result.

A typical use case for dataflow on GCP is to transfer large volume of data between different storage services or message queues while apply data transformation.

## PoC Overview

In this PoC, a dataflow job is created with starts by generating mock transaction data which contains basic fields including a UUID for transaction event, customer, amount, timestamp.
