---
Title: ELK Stack
Description: >
 Elacticsearch, Kibana, Logstash
---

## Elasticsearch

### How data processing before building Index

1. Operation of `Text field` and `Analyzer`
    + Behind the full-text search mechanism, how text processing through `Lucene`
2. Dynamic Mapping practical tips
    + Uniform naming convention -> `dynamic_templates`
    + carefully setting `dynamic templates`
    + ***Turn off*** dynamic fields mapping
      + X ~~`dynamic: false`~~
      + V `dynamic: strick`
    + ***Turn off*** `date` or `number` automatic judgment
3. Index Template Recommendation
   <!-- + -->
4. Index Alias

### keyword type vs. text datatype

[When to use the keyword type vs. text datatype in Elasticsearch | ObjectRocket](https://kb.objectrocket.com/elasticsearch/when-to-use-the-keyword-type-vs-text-datatype-in-elasticsearch)

### Ref

+ [Elasticsearch Index 管理與效能優化技巧 - YouTube](https://www.youtube.com/watch?v=dVUMqi5knuo)

## Kibana

Kibana is a free and open user interface that lets you visualize your Elasticsearch data and navigate the Elastic Stack. Do anything from tracking query load to understanding how requests flow through your apps.

+ UI Dashboard
+ Widgets / Visualization

## Logstash

+ Input / Transform /stash

## Application Architecture Reference

![1bdee42](./1bdee42.png)
![bc31ac7](./bc31ac7.png)
\\( \uparrow \\) [image ref: Building a real-time elastic search engine using Python, Easticsearch, React, Redux, and K8](https://faun.pub/building-a-real-time-elastic-search-engine-using-python-32e05bcb9140)

![0eccb35](./0eccb35.png)
\\( \uparrow \\)  [image ref: Using Amazon ElasticSearch to Improve Performance when Querying Data in MySQL](https://blog.clearscale.com/amazon-elasticsearch-mysql-performance/)
