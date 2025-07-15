# AIEB_final_project

## Project Overview
This project is an "AI-powered PDF Document Q&A System" that allows users to upload PDF files (such as 10-K financial reports) and interact with their content using natural language. The project features two main versions:
- **OpenAI Version** (`chatbot_openai.py`): Powered by OpenAI GPT-4o
- **Gemini Version** (`V2_chat_with_pdf_gemini_with_history.py`): Powered by Google Gemini-2.0-flash

## Features
- Upload and parse multiple PDF files
- Document chunking and vector storage (FAISS)
- Context-aware intelligent Q&A
- Multi-turn conversation with chat history
- Source citation for answers
- Streamlit-based user interface

## Model Details

### OpenAI Version
- **LLM**: GPT-4o (via `langchain_openai.ChatOpenAI`)
- **Embedding Model**: OpenAIEmbeddings
- **Vector Store**: FAISS
- **Chunking Strategy**: 500 characters per chunk, 50 characters overlap
- **Retrieval Chain**: RetrievalQA (`chain_type="stuff"`)
- **Prompt**: Acts as a professional financial analyst, strictly referencing 10-K documents, no speculation or external knowledge

### Gemini Version
- **LLM**: Gemini-2.0-flash (via `langchain_google_genai.ChatGoogleGenerativeAI`)
- **Embedding Model**: GoogleGenerativeAIEmbeddings (`model="models/embedding-001"`)
- **Vector Store**: FAISS
- **Chunking Strategy**: 500 characters per chunk, 50 characters overlap
- **Retrieval Chain**: ConversationalRetrievalChain, supports multi-turn memory
- **Prompt**: Answers only based on document content, clearly states when information is insufficient

## Requirements

- Python 3.8+
- Main dependencies:
  - streamlit
  - langchain
  - langchain_community
  - langchain_openai
  - langchain_google_genai
  - faiss-cpu
  - google-generativeai
  - See `requirements.txt` for full list

## Quick Start

1. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

2. **Set API Keys**
   - OpenAI Version: Set `OPENAI_API_KEY` in `chatbot_openai.py`
   - Gemini Version: Set `GOOGLE_API_KEY` in `V2_chat_with_pdf_gemini_with_history.py`

3. **Run Streamlit App**
   ```bash
   streamlit run chatbot_openai.py
   # or
   streamlit run V2_chat_with_pdf_gemini_with_history.py
   ```

4. **Upload your PDFs and start chatting!**

## Project Structure

- `chatbot_openai.py` — Main program for OpenAI version
- `V2_chat_with_pdf_gemini_with_history.py` — Main program for Gemini version
- `10k_files/` — Example PDF files

## Notes
- Do not upload PDFs containing sensitive information
- Keep your API keys secure
- For research and educational use only, not for commercial purposes

## Contact
For questions or suggestions, please contact the author. 
