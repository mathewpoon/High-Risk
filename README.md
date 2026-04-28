# Summary

This repo contains the code for the final project for UT Austin AI In Healthcare Class.

(Presentation added in repo: TBD)

Contributers
  - Ali Gardezi: ali.imam.gardezi@gmail.com
  - Ganesh Devaraj: ganesh.devaraj.msai@utexas.edu
  - Kishore Kolli: kkolli@utexas.edu 

# Project

The Project compared two implementations of Graph RAG.

-  Microsoft GraphRAG (https://microsoft.github.io/graphrag/)
-  StanfordCoreNLP + Neo4J (https://stanfordnlp.github.io/CoreNLP/, https://neo4j.com/)

The steps executed were,

- Indexing data into a Graph
- For a question relevant to the data, extract data relevant to answering those questions from the Graph
- Provide the question, data extracted from Graph to an LLM.
- The LLM will return the answer
   

# Approaches

We tried two approaches.

- Approach#1
  - Created our own Graph RAG solution using StanfordNLP to extract entities and relationships.
  - Used Neo4J to create a Graph for those entities and relationships.
  - For a question, extracted entities and relationships from the Graph.
  - Created a Prompt with the question, the extracted entities and relationships from the Graph and asked OpenAI to return an answer based on the data provided.
- Approach#2
  - Used Microsoft Graph RAG to load data
  - Used Microsoft Graph RAG local query to provide answers to questions


# Dataset

The Dataset that we used was the Anatomy Book by Gray sourced from https://huggingface.co/MedRAG

The questions that we used to test the solutions were sourced from https://github.com/Teddy-XiongGZ/MIRAGE/blob/main/rawdata/mmlu/data/test/anatomy_test.csv


# Observations

## Microsoft GraphRAG

- Execution time for building the graph (entities, relationships and communities) for the Anatomy book - approx 2 hr 30 min
- Cost to run Open AI GPT-4o - approx 55 dollars
- No of entities extracted 35652
- No of relationships extracted 85968
- No of communities built 12950

## Stanford NLP + Neo4J 

- Execution time for building the graph (entities, relationships) for the Anatomy book - approx 8 hrs
- Cost to run - 0 dollars - since both Stanford NLP server and Neo4J server were run locally
- No of entities extracted 78075
- No of relationships extracted 195756

# Results

- Stanford NLP + Neo4J was able to answer 53 out of 135 questions correctly
- Microsoft GraphRAG was able to answer 114 out of 135 questions correctly

# Files/Folders in the repo

- Project_Graph_Stanford_CoreNLP.ipynb
  -  notebook for our Stanford Core NLP + Neo4J Implementation
- Microsft_Graph_RAG_Anatomy.ipynb
  -  notebook for our Microsft GraphRAG Implementation
- document-index.ipynb
  -  notebook for another approach where we tried extracting entity and relationships using ClinicalBERT
- anatomy_test.csv
  -  question list with answers
- microsoft_graph_rag_answers_comparison_to_answer_key.csv
  -  breakdown of answers to questions using Microsoft GraphRAG
- stanford_nlp_graph_answers_comparison_to_answer_key.csv
  -  breakdown of answers to questions using StanfordCoreNLP + Neo4J
- ./anatomy_questions
  -  folder containing questions seperated into individual files
- ./anatomy_answers_graph_rag
  -  folder containing answers retuned for each question from Microsft GraphRAG
- ./anatomy_answers_stanford_nlp  
  - folder containing answers retuned for each question from StanfordCoreNLP + Neo4J
- ./anatomy_stanford_nlp_open_ai_prompts
  - fodler containing the open ai prompts used to get the answers to the question using StanfordCoreNLP + Neo4J
