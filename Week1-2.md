# TTDS Week1.2

Created: 2025年9月21日 11:29
Class: TTDS
Content: Chapter2
Learning time: 2.5

# Chapter2 Architecture of a Search Engine

## 2.1 What is an Architecture

An example of an architecture used to
provide a standardfor integrating search and related language technology components is **UIMA** (Unstructured Information Management Architecture).

### Two primary goals of a search engine

- Effectiveness/quality
- Efficiency/speed

## 2.2 Basic Building Blocks

Two major functions: 

### **indexing process**(searching)

- **Text Acquisition**: identify the documents will be searched(source of info: crawling/scanning the Web/corporate intranet/desktop)
- **Document Data Store:** contains the text and metadata(type/structure/doc length)
- **Text Transformation** component transforms documents into ***index terms*** or ***features**.*  Output: index vocabulary
- **Index Creation**: needs to be efficiently updated. Most common method is **Inverted indexes/incerted files**

![截屏2025-09-21 11.45.21.png](TTDS%20Week1%202%202757b2c283728014b103c7eee74967d6/%E6%88%AA%E5%B1%8F2025-09-21_11.45.21.png)

### query process(ranking)

- user interaction
    1. accepting the user’s query and transforming it into index terms
    2. take the ranked list of documents from the search engine and organize it into the results(**snippets** used to summarize doc).
    3. provide techniques for refining the query
- **ranking(core)**
    1. transformed query from the user interaction component and **generates** a ranked list of documents using scores based on a retrieval model.
    2. The efficiency of ranking depends
    on the indexes, and the effectiveness depends on the retrieval model.
- evaluation
    1. record and analyze user behavior using log data
    2. tune and improve the ranking component

![截屏2025-09-21 12.06.43.png](TTDS%20Week1%202%202757b2c283728014b103c7eee74967d6/%E6%88%AA%E5%B1%8F2025-09-21_12.06.43.png)

## 2.3 Breaking It Down

![image.png](TTDS%20Week1%202%202757b2c283728014b103c7eee74967d6/image.png)

### 2.3.1 Text Acquisition

- Crawler/general web crawler
    
    there are significant challenges in designing a web crawler that can efficiently handle the huge volume of new pages on the Web, while at the same time ensuring that pages that may have changed
    
- Feeds
    1. real-time stream of documents. eg.news stories and updates
    2. **RSS** is a common standard and actually refers to a family of standards with similar names (and the same initials), such as Really Simple Syndication or Rich Site Summary
- Conversion
    1. utilities are available to convert various formats into text
    2. converted into a consistent encoding scheme: ASCII 7 or 8 bits; Unicode 16bits
- Document data store
    1. stored in compressed form for efficiency, for fast retrieved documents
    2. structured data consists of metadata and other info extract from the documents, such as from **link and anchor text**

### 2.3.2 Text Transformation

- Parser
    1. recognize structural elements(title, figures, links) from the sequence of text tokens in the document
    2. **Tokenizing** is the first step, potentially affecting retrieval
    3. The document parser uses knowledge of the **syntax** **of the markup language to identify the structure. eg. XML, HTML #tags
- Stopping
    1. removing common words from the stream of tokens that become index terms. eg.*function words*
    2. difficult to decide how many words to include on the **stopword list**
    3. ⚠️to be or not to be—> all stop word list, longer lists for default processing of query text
- Stemming
    1. **group** words that are derived from a common stem. fish, fishes, fishing
    2. increase the likelihood that words used in queries and documents
    will match.
    3. small improvements for languages with little word variation such as Chinese
- link extraction and analysis
    1. link analysis algorithms such as PageRank provide the authority of a page
    2. Anchor text
- Information extraction
    1. identify index terms
    2. technique：name entity recognizers
- Classifier
    1. assign predefined label to documents
    2. clustering without predefined catagories

### 2.3.3 Index Creation

- Document statistics
    - counts of index term occurrences, positions of index terms, length of documents
    - stored in lookup tables
- Weighting
    - reflect the importance of words in documents
    - **tf.idf:** based on a combination of the frequency or count of index term occurrences in a document (the *term frequency*, or *tf* ) and the frequency of index term occurrence over the entire collection of documents (*inverse document frequency*, or *idf* ).
    - A typical formula for ***idf*** is log *N*/*n*, where *N* is the total number of documents indexed by the search engine and *n* is the number of documents that contain a particular term.
- **Inversion**
    - document-term information —> term-document information, for the creation of **inverted indexes**
    - challenge: efficiency(large numbers of documents+updated new documents)
- Index distribution
    - parallel: document distribution and term distribution
    - replication
- [ ]  peer-to-peer search

## 2.3.4 User Interaction

![截屏2025-09-21 12.06.43.png](TTDS%20Week1%202%202757b2c283728014b103c7eee74967d6/%E6%88%AA%E5%B1%8F2025-09-21_12.06.43.png)

- Query input
    - operator: clarify meaning. eg.quotes
    - keywords: “search engines”may produce a better result with a web search engine than the query “what are typical implementation techniques and data structures used in search engines”.
    - Boolean query langauge
- Query transformation
    - improve initial query
    - Tokenizing, stopping, and stemming must be
    done on the query text to produce index terms that are comparable to the document terms.
    - Spell checking and query suggestion, which often leverage query logs.
    - query expansion
    - relevance feedback
- Results output
    - generating **snippets**, **highlighting** important words and passages…

## 2.3.5 Ranking

- Scoring/*query processing*
    - related to topic and user relevance
    - basic form of the document score:
    
    $$
    \sum_i q_i \cdot d_i 
    $$
    
     $q_i$  is the query term weight of the $*i*$th term, and $*d_i$* is the document term weight(generally similar to *tf.idf* weights).
    
    - BM25 & query likelihood
- Optimization: throughput
    - *term-at-a-time* scoring
    - *document-at-a-time* scoring
- Distribution
    - query broker
    - caching

## 2.3.6 Evaluation

- Logging
    - spell checking, query suggestion, ad.
    - dwell time
- Ranking analysis
    - emphasize the quality of the top-ranked documents
- performance analysis
    - response time, throughput
    - distribution: network usage
    - mathematical simulations(==test collections in ranking analysis)