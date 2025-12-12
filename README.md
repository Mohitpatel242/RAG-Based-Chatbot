# RAG-Based-Chatbot
This is a Agentic RAG System the sophisticated application that moves beyond simple question-answering by using an autonomous agent (ReAct pattern) that can decide where to look for information (your local documents or Wikipedia).

The system is built on LangGraph, which treats the AI workflow as a state machine. This allows for loops, decision-making, and maintaining "state" (memory) as the AI processes a request.

Decision Brain (reactnode.py & graph_builder.py):

Unlike a standard RAG that always searches documents, your system uses a ReAct Agent.

The agent has access to two specific tools:

Retriever Tool: Searches your uploaded PDFs/URLs via the vector store.

Wikipedia Tool: Searches Wikipedia for general knowledge if the answer isn't in your docs.

The GraphBuilder constructs the workflow, defining the flow from the retriever node to the responder.

Data Pipeline (document_processor.py & vectorstore.py):

Ingestion: The DocumentProcessor handles multiple formats. It can scrape URLs, read PDF directories, and parse TXT files.

Chunking: It uses RecursiveCharacterTextSplitter to break text into manageable 500-character chunks with overlap to preserve context.

Storage: The VectorStore embeds these chunks using OpenAIEmbeddings and saves them into a FAISS index for fast similarity search.

User Interface (streamlit_app.py):

Provides a web interface using Streamlit. It manages session state (history of chats), caches the heavy model initialization, and displays retrieved source documents alongside the answer.
