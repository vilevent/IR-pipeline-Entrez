# Information Retrieval Pipeline
> **Python** project from Spring 2022 Directed Independent Study

My project stemmed from a cross-departmental collaboration that focused on "Exploring the Feasibility of Automating Biocuration for Neuropharmacology and Zebrafish (*Danio rerio*)."

> #### ***Further details are found within the report.***

### Problem
It's difficult for bio-researchers to manually sort through millions of published articles in order to find the most **relevant**, **reputable** ones. Ideally, the gathered articles should contain information that can be used to develop other experiments and direct further research for topics such as *Ivermectin regulation of the GABA pathway*.

### Motivation
Programmatically establishing an information retrieval (IR) pipeline for future bio-researchers in the growing area of neuropharmacology.

### Data
The primary data sources were two biomedical literature databases: [**PubMed**](https://pubmed.ncbi.nlm.nih.gov/) and [**PubMed Central**](https://www.ncbi.nlm.nih.gov/pmc/) (PMC). Abstracts are found in PubMed, and full-text articles are found in PMC.

### Tools
- **Biopython** library, Entrez package
- E-utilities: *ESearch*, *ESummary*, *ELink*

**Use cases:**

*ESearch* - retrieving a set of article IDs corresponding to a search query as well as retrieving the counts returned by that query.

*ESummary* - extracting the publication date for each article ID that was retrieved from ESearch.

*ELink* - determining the citation counts for each article by using the connections/links between articles within the Entrez databases.

### IR Pipeline
***Inputs***: Search queries for a database (PubMed, PMC).
- Example of a query: "GABA AND Ivermectin NOT COVID-19"

![pipeline](https://user-images.githubusercontent.com/96803412/168202930-2967e659-2f70-4d8b-8191-1052bd4e781c.png)

***Data Processing***: Keeping only the articles that have **at least 25 citation counts** and thus filtering out the rest that do not meet this criterion. Establishing this criterion was important as it signifies that an article is reputable. This **reputability** is significant for when bio-researchers examine these publications for their own research work.

***Outputs***: Top-k articles per query. (This k value is specified by the user.)

### Functions created for the Pipeline:
```python
esummary_info(in_webenv_key, in_query_key, db_name)
```

```python
get_published_dates(esummary_rec)
```

```python 
get_pmcids(esummary_rec)
```

```python
get_pmids(esummary_rec)
```

```python
get_query_info_no_genes(query_in, db_name)
```

```python
get_query_info(query_in, genes, db_name)
```

```python
cited_cnt_table(df_summary, db_name)
```

```python 
get_top_k(df, k_val)
```

##

### Bioconcept Annotations
Since a **biocurator tool** would auto-annotate biomedical articles from literature databases, we investigated [**PubTator Central**](https://www.ncbi.nlm.nih.gov/research/pubtator/) (PTC) and the annotations it provided (via API calls) for a set of articles.

```python
get_pt_annotations(str_of_ids)
```
This function *get_pt_annotations* was created to retrieve the **PubTator annotations** when provided a set of IDs, which can be either ***PMIDs*** or ***PMCIDs***. 

Then, the user can extract the annotations individually to process and/or visualize them. For example,

![plot](https://user-images.githubusercontent.com/96803412/168210107-09f39d75-337c-462b-b474-462292259d44.png)


