# TTDS Week1.1

Created: 2025年9月20日 21:43
Class: TTDS
Book: https://ciir.cs.umass.edu/downloads/SEIRiP.pdf
Content: Chapter 1
Learning time: 1.6

# Overview

**Chapter 1**: high-level review of the field of information retrieval and its relationship to search engines 

**Chapter2**: architecture of a search engine.

## **1.1 What Is Information Retrieval?**

**Salton, 1968**: Information retrieval is a field concerned with the structure, analysis, organization, storage, searching, and retrieval of information.

<aside>
💡

Mainly focus on **structural** documents, such as books, email, scholarly papers…

**Attributes/fields**: the elements of this structure.

Easy to compare/queries values of these attributes

</aside>

⚠️ Long text does’t have internal structure.

⚠️ Media data should also be considered.  eg.scanned document, image, music…

### Application scenario:

- Vertical search: Web Search on particular topic.
- Enterprise search: corporate intranet.
- Web pages
- Desktop search
- Peer-to-peer search: This type of search began as a file sharing tool for music but can be used in any community based on shared interests, or even shared locality in the case of mobile devices.
- Any collection of information

### Tasks of IR

- user query/ad hoc search
- filtering: detecting stories of interest based on a person’s interests and providing an alert
- classification: assign labels to doc
- question answering

## 1.2 The Big Issue

### Relevance/effective ranking algorithms

😭Comparing the text of query with the text of document and looking for an **exact** match produce poor results(*vocabulary mismatch problem*). 

- **topic relevance** and **user relevance**
- **🔧retrieval models**, which **i**s the basis of the **ranking algorithm**. In practice, user relevance should be incorporated.
- **⚠️retrieval models** typically model the **statistical properties(frequency, count)** of text rather than the **linguistic structure (but it should be considered)**

### Evaluation

- **precision**: the proportion of retrieved documents that are relevant.
- **recall**: the proportion of relevant documents that are retrieved. (test collections of documents)
- **Focus**: log data from user interaction, such as clickthrough data.

### The emphasis on users and their information needs.

- An information need is the underlying cause of the query that a person submits to a search engine. eg. cats→animal/Broadway musical
- Techniques: query suggestion, query expansion, and relevance feedback

## 1.3 Search Engines

- A number of configurations of Search engines: Google, Yahoo!, Lemur, Indri, Galago (crawl, data mining, clustering, Open source)

### **Big issues: far beyond issues of information retrieval**

- Performance (large-scale,operational environements)
    - response time, query throughput, indexing speed
- Incorporating new data: Coverage and freshness
- Scalability: growing with data and users
- Adaptability: customization
- Spamdexing

## 1.4 Search Engineers

designing, implementing, modifying, extend, maintain