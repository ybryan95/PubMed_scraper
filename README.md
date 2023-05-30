PubMed Gene-Search and Abstract Analysis
This python script contains multiple methods aimed at fetching gene-related articles from PubMed and creating visualizations (word clouds) from the abstracts. The code extracts genes related to autism while excluding any mention of cancer or tumor.

Table of Contents
Key Functions
Usage
Dependencies
Acknowledgements
Disclaimer
Key Functions <a name = "key-functions"></a>
gene_to_search(element, fullName): This function generates search terms to be used in querying PubMed, focusing on articles related to the gene name or its full name, and terms related to autism, but not cancer or tumors.
gene_fullName(gene_abbr): This function takes a gene abbreviation and queries the mygene.info API to get the full gene name.
generate_wordcloud(input_text, nlp1, nlp2, nlp3): This function creates a word cloud based on the input text. It uses three different spaCy models for Named Entity Recognition (NER) to identify relevant entities (like genes, diseases, and taxons), and also highlights specific terms such as 'stem cell' and 'iPSC'.
fetch_abstract(pmid): Fetches the abstract for a given PubMed ID (pmid) using the Entrez API.
search_query(query, fullName_list, gene, i): This function takes a search query, a list of gene full names, a gene, and an index. It searches the PubMed database using the Entrez API, and returns a list of articles including their URLs, DOIs, titles, publication years, and full abstracts.
The script then uses the Python docx library to export the data (gene names and corresponding article information) to a Word (.docx) document, and creates a word cloud for each abstract.

Usage <a name = "usage"></a>
Load the required spaCy models and PubMed toolkit.
Input the gene of interest (e.g., 'CIC') and fetch related articles from PubMed.
Generate a DataFrame with 'gene' and 'info' columns.
Iterate through the DataFrame, create a word cloud for each abstract and append it to a Word document.
Save the Word document. An additional function is available to remove images and save a text-only version of the document.
Dependencies <a name = "dependencies"></a>
Python 3.6 or above
pandas
requests
Bio.Entrez from biopython
spacy (with the "en_ner_bionlp13cg_md", "en_ner_bc5cdr_md", and "en_ner_craft_md" models)
WordCloud from wordcloud
Document from docx
Image from PIL
Note: Please ensure to update the email in search_query function with your own email address before running the script. You may also need to adjust the sleep time between requests to meet API guidelines.

Acknowledgements <a name = "acknowledgements"></a>
This script uses the mygene.info API, the Entrez Programming Utilities (E-utilities), and the PubMed API. Please respect their terms of use.

Disclaimer <a name = "disclaimer"></a>
This script is provided as is, without warranty of any kind. Use of the information herein is at the user's own risk. Users should make their own evaluation of the accuracy and adequacy of those information.
