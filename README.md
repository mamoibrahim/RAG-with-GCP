# RAG-with-GCP


## Grounding in GenAI

Grounding in Generative AI refers to the practice of making AI-generated outputs based on real, verifiable, and specific data or context. It ensures that responses are not just plausible-sounding, but actually reliable and factually accurate.

Grounding is especially critical in high-stakes domains like healthcare, law, education, and finance, where incorrect or hallucinated content can cause harm.

Types of Grounding

## Data Grounding

AI uses a structured database or real-time API to answer questions.

Example: Pulling stock prices from a finance API before generating a summary.

## Document Grounding (RAG)

Retrieval-Augmented Generation (RAG) pulls text from a set of documents (e.g., PDFs, manuals, articles) to answer user queries.

Example: Answering customer questions based on a product manual.

## User Context Grounding

Using user-specific inputs or history to tailor responses.

Example: Personalizing a workout plan based on previous sessions.




# Tools and Libraries for Grounding

LangChain – For chaining LLMs and retrievers.

LlamaIndex – Optimized for document indexing and RAG.

FAISS, Weaviate, Pinecone – Vector stores.

OpenAI, HuggingFace, Cohere – For embeddings and LLMs.


# Example  


![image](https://github.com/user-attachments/assets/cbf9a315-28ac-4172-87e1-7fd69ed6cf1a)
.
.
![image](https://github.com/user-attachments/assets/e292def4-9abf-4935-bff0-7e1df9619924)


# 1) Data retrieval


Retrieve data that is relevant to the problem.

This data can include user data for the logged in user and other information that is not found in the foundation model.

# 2) Augmented prompt

Add the data to the prompt.

In your prompt, you include the retrieved information as context, and tell the model that the data is trusted and that the response can use the information.


# 3) Generated response


The generated response is more relevant and reliable.

The model generates a response, utilizing both information from the model and the retrieved data that the app provided in the prompt.


#  detailed view of a RAG architecture on Google Cloud:

![image](https://github.com/user-attachments/assets/792e07eb-9c5e-4c6f-9a2a-3434653f08ad)

![image](https://github.com/user-attachments/assets/12f50358-22f5-43b2-9a6a-98258ab5d748)

1-Data is uploaded to a Cloud Storage bucket. The data source might be an application user performing an upload, database ingestion, or streaming data.

2-When data is uploaded, a notification is sent to a Pub/Sub topic.

3-Pub/Sub triggers a Cloud Run job to process the uploaded data.

4-Cloud Run starts the job by using configuration data that's stored in an AlloyDB for PostgreSQL database.

5-The Cloud Run job uses Document AI to prepare the data for further processing.

For example, the preparation can include parsing the data, converting the data to the required format, and dividing the data into chunks.

6-The Cloud Run job uses the Vertex AI Embeddings for Text model to create vector embeddings of the ingested data.

7-Cloud Run stores the embeddings in an AlloyDB for PostgreSQL database that has the pgvector extension enabled.

When the serving subsystem processes user requests, it uses the embeddings in the vector database to retrieve relevant domain-specific data.


# Serving subsystem

![image](https://github.com/user-attachments/assets/636e66e5-e4f7-4f3c-9a9d-2b21d9ab5aff)





![image](https://github.com/user-attachments/assets/2d2c0fd9-8903-4045-987d-bff1b3c0c4f2)
