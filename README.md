<a href="https://allenai.github.io/scispacy/"><img src="https://img.shields.io/badge/SciSpacy-FFCA28?style=flat-square&logo=SciSpacy&logoColor=white"/>
<a href="https://biopython.org/docs/1.76/api/Bio.Entrez.html"><img src="https://img.shields.io/badge/BioPython.Entrez-33A0FF?style=flat-square&logo=BioPython-Entrez&logoColor=white"/> <a href="https://pubmed.ncbi.nlm.nih.gov/help/"><img src="https://img.shields.io/badge/PubMed.SearchGuide-E7E1E1?style=flat-square&logo=PubMed.SearchGuide&logoColor=black"/> <a href="https://python-docx.readthedocs.io/en/latest/"><img src="https://img.shields.io/badge/PythonDocx-B2FDFA?style=flat-square&logo=pythonDocx&logoColor=white"/> <a href="https://mygene.info/"><img src="https://img.shields.io/badge/MyGene.io-BCFDB2?style=flat-square&logo=MyGene.io&logoColor=white"/>

# PubMed Gene-Search and Abstract Analysis 

This python script contains multiple methods aimed at fetching gene-related articles from PubMed and creating visualizations (word clouds) from the abstracts. The code extracts genes related to autism while excluding any mention of cancer or tumor. 

## Table of Contents
- [Key Functions](#key-functions)
- [Usage](#usage)
- [Key Dependencies](#dependencies)
- [Acknowledgements](#acknowledgements)
- [Disclaimer](#disclaimer)

## Key Functions <a name = "key-functions"></a>
1. `gene_to_search(element, fullName)`: This function generates search terms to be used in querying PubMed, focusing on articles related to the gene name or its full name, and terms related to autism, but not cancer or tumors.
2. `gene_fullName(gene_abbr)`: This function takes a gene abbreviation and queries the mygene.info API to get the full gene name.
3. `generate_wordcloud(input_text, nlp1, nlp2, nlp3)`: This function creates a word cloud based on the input text. It uses three different spaCy models for Named Entity Recognition (NER) to identify relevant entities (like genes, diseases, and taxons), and also highlights specific terms such as 'stem cell' and 'iPSC'.
4. `fetch_abstract(pmid)`: Fetches the abstract for a given PubMed ID (pmid) using the Entrez API.
5. `search_query(query, fullName_list, gene, i)`: This function takes a search query, a list of gene full names, a gene, and an index. It searches the PubMed database using the Entrez API, and returns a list of articles including their URLs, DOIs, titles, publication years, and full abstracts.

The script then uses the Python docx library to export the data (gene names and corresponding article information) to a Word (.docx) document, and creates a word cloud for each abstract. 

## Usage <a name = "usage"></a>

1. Load the required spaCy models and PubMed toolkit. Please change the email used for passing search queries to your PubMed account email.
![image](https://github.com/ybryan95/PubMed_scraping_NoGPT/assets/123009743/f3f1a964-f1ef-4b9b-a9fa-cfd82f0521b5)

2. Input the gene of interest (e.g., 'CIC') and fetch related articles from PubMed. (Ensure your choice of keywords like genes are in the first column of the TF.xlsx file and it is placed in the same folder with TF_Docx.ipynb)
![image](https://github.com/ybryan95/PubMed_scraping_NoGPT/assets/123009743/e4d4f63e-77bf-4c66-8db3-3b0c1c0f6045)
3. Generate a data frame with 'gene' and 'info' columns.
4. Iterate through the DataFrame, create a word cloud for each abstract, and append it to a Word document. The selection of keywords is performed by choosing Entity types in sci-spacy models (https://allenai.github.io/scispacy/). You will need to download their models for use in TF_Docx.ipynb
![image](https://github.com/ybryan95/PubMed_scraping_NoGPT/assets/123009743/3df7bb11-82bf-4318-a622-c3f879f89f75)

> **_NOTE:_** **After downloading your interest in models, they are implemented through the section in the code:**
![image](https://github.com/ybryan95/PubMed_scraping_NoGPT/assets/123009743/a38296f1-9cd1-49c9-bffc-a472fc31e561)


> **_NOTE:_** **Notice how the entity types shown on the sci-spacy page are used in the code.**
![image](https://github.com/ybryan95/PubMed_scraping_NoGPT/assets/123009743/58fd4f43-30b8-4662-9a52-61b56da49e8d)



5. Save the Word document. An additional function is available to remove images and save a text-only version of the document.
6. For example, a gene named "CIC" and its full name "Capicua Transcriptional Repressor" would generate two queries - "(CIC[Title/Abstract]) AND ((AUTISM[Title/Abstract]) OR (autistic[Title/Abstract])) NOT (CANCER[Title/Abstract]) NOT (TUMOR[Title/Abstract])" and a similar one with the full gene name.
![image](https://github.com/ybryan95/PubMed_scraping_NoGPT/assets/123009743/c3eb8508-67b4-4e77-99b3-c38cf97fb39f)
> **_NOTE:_** **To personalize the usage, I suggest practicing and getting familiar with an advanced search on PubMed (https://pubmed.ncbi.nlm.nih.gov/advanced/)**

> **_NOTE:_** **For example, notice how the placement of parentheses makes the search query yield 2 or 16235 results.**
![image](https://github.com/ybryan95/PubMed_scraping_NoGPT/assets/123009743/d6af717f-9084-4739-bf37-4054a6b03cb6)

> **_NOTE:_** **The search query you will be passing in the TF_Docx.ipynb provided will appear on the section of the code shown:**
![image](https://github.com/ybryan95/PubMed_scraping_NoGPT/assets/123009743/cf1092dc-78ea-4976-8a76-a91ca6a56975)




## Dependencies <a name = "dependencies"></a>

- Python 3.6 or above
- `pandas` 
- `requests`
- `Bio.Entrez` from `biopython`
- `spacy` (with the "en_ner_bionlp13cg_md", "en_ner_bc5cdr_md", and "en_ner_craft_md" models)
- `WordCloud` from `wordcloud`
- `Document` from `docx`
- `Image` from `PIL`

> **Note:** Please ensure to update the email in `search_query` function with your own email address before running the script. You may also need to adjust the sleep time between requests to meet API guidelines (Refer to https://pubmed.ncbi.nlm.nih.gov/robots.txt).  

## Acknowledgements <a name = "acknowledgements"></a>

This script uses the mygene.info API, the Entrez Programming Utilities (E-utilities), and the PubMed API. Please respect their terms of use. 

## Disclaimer <a name = "disclaimer"></a>

This script is provided as is, without warranty of any kind. Use of the information herein is at the user's own risk. Users should make their own evaluation of the accuracy and adequacy of those information.

