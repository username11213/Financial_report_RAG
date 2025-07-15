# Technical Note

## System Architecture

This project is designed as an AI-powered PDF document question-answering system, supporting both OpenAI and Google Gemini large language models. The system is implemented using Python and Streamlit, providing an interactive web interface for users to upload PDF files and engage in natural language conversations about their content. The architecture is modular, separating document processing, vector storage, retrieval, and language model inference.

## Model Selection Rationale

Two state-of-the-art large language models are integrated: OpenAI's GPT-4o and Google's Gemini-2.0-flash. The OpenAI version leverages the proven capabilities of GPT-4o for high-quality, context-aware responses, particularly suitable for financial and technical documents. The Gemini version is included to provide an alternative based on Google's generative AI, offering diversity in model behavior and potential improvements in certain document types or question styles. Both models are accessed via their respective APIs, ensuring up-to-date performance and security.

## Data Flow and Processing

1. **PDF Upload and Parsing**: Users upload one or more PDF files through the Streamlit interface. The system uses `PyPDFLoader` to extract text from each document.
2. **Text Chunking**: Extracted text is divided into overlapping chunks (500 characters per chunk, 50 characters overlap) using a recursive character splitter. This approach preserves context and improves retrieval accuracy.
3. **Embedding and Vector Storage**: Each text chunk is converted into a vector representation using either OpenAIEmbeddings or GoogleGenerativeAIEmbeddings, depending on the selected model. The vectors are stored in a FAISS index for efficient similarity search.
4. **Retrieval and Q&A**: When a user submits a question, the system retrieves the most relevant document chunks using vector similarity. The selected language model then generates an answer, strictly based on the retrieved content. The OpenAI version uses a RetrievalQA chain, while the Gemini version employs a ConversationalRetrievalChain to support multi-turn dialogue.
5. **Response and Citation**: The answer is displayed to the user, with citations or excerpts from the source documents to ensure transparency and traceability.

## Key Implementation Details

- **Prompt Engineering**: Both versions use carefully crafted prompts to ensure the models answer only based on the provided documents, avoiding speculation or hallucination. The OpenAI version is tailored for financial analysis, while the Gemini version emphasizes clarity and acknowledges when information is insufficient.
- **Session Management**: Chat history and vector stores are maintained in Streamlit's session state, enabling smooth multi-turn interactions and efficient resource usage.
- **Error Handling**: The system includes robust error handling for file uploads, document parsing, and API interactions, providing informative feedback to users.
- **Security**: API keys are required for both OpenAI and Gemini services. Users are advised to keep these keys secure and avoid uploading sensitive documents.

## Conclusion

This project demonstrates a practical application of large language models for document analysis and question answering. By combining advanced retrieval techniques with powerful generative models, it enables users to extract valuable insights from complex PDF documents in an accessible and transparent manner. 
