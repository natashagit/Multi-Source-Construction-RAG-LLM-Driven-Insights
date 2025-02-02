# Contech-Hackathon
The solution presented effectively combines structured data (RDF-based knowledge graphs) and unstructured data (PDF documents) using advanced NLP techniques to create a comprehensive and responsive chatbot. Here's how the components interact to achieve the desired functionality:

![Architecture](./images.png)


### **Summary of Functionality**

1. **PDF Parsing and Sentence Embedding**
    - The unstructured data (PDFs) is parsed into text using `PyPDFLoader`.
    - Extracted text is segmented into sentences using a regex-based approach.
    - Each sentence is encoded into high-dimensional embeddings using the SentenceTransformer model (`all-MiniLM-L6-v2`).
2. **Structured Data Handling**
    - A CSV file containing structured data is processed.
    - Rows are dynamically converted into natural language sentences.
    - Sentences are embedded similarly to the unstructured data.
3. **Query Processing**
    - A user query is embedded using the same SentenceTransformer model.
    - Cosine similarity is computed between the query embedding and both structured and unstructured data embeddings.
    - The top results are identified from both datasets.
4. **Contextual Response Generation**
    - The top matches from both data sources are combined into a unified context.
    - The `openai.ChatCompletion` API with the GPT-4 model synthesizes the final response, providing a seamless summary or answer based on the integrated context.

![image.png](attachment:fb8719dd-0012-4a23-a5bf-65ec362b8dba:image.png)

### **Implementation Highlights**

- **Integration of Data Sources:** Combines structured RDF-like data and unstructured textual content seamlessly by normalizing them into the same representational format (sentence embeddings).
- **Accuracy and Relevance:** Uses cosine similarity to match user queries with both data sources, ensuring relevance in responses.
- **Dynamic Context Creation:** Unifies data sources into a single context for a comprehensive response, enabling better understanding and completeness.

### **Output Example**

For the query:

> "What is the effective date and expiration date of this certificate 120486116T001?"
> 

The chatbot provides a detailed response summarizing both structured and unstructured data, noting mismatches (if any) and emphasizing document consistency.

### **Possible Enhancements**

1. **Knowledge Graph Integration:** Use SPARQL queries directly on RDF graphs for richer and more complex relationships.
2. **Query Understanding:** Leverage semantic parsing to improve the handling of complex and multi-part questions.
3. **Scalability:** Optimize the pipeline to handle large datasets efficiently using batch processing or vector search libraries like FAISS.
