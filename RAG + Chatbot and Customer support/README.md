# RAG-Powered Chatbot & Customer Support Automation

Single cohesive workflow that ingests documents from Google Drive, indexes them in a vector DB (Pinecone), and exposes that knowledge to an LLM-powered agent for both interactive chat and automated customer-support email replies.

---

## Overview

The workflow continuously transforms company documents (e.g., FAQs, policies) into **vector embeddings** stored in Pinecone. These vectors are later retrieved by an AI agent whenever a user asks a question in chat or when a customer sends a support email.

By combining **retrieval-augmented generation (RAG)** with workflow automation, the system ensures every response is accurate, contextual, and consistent with internal policies.

---

## Core Capabilities

--  &nbsp;**Dynamic Knowledge Ingestion**  
  Documents added to a Google Drive folder are automatically vectorized, chunked, and indexed in Pinecone.

--  &nbsp;**Context-Aware Chat Agent**  
  Users can interact with a chatbot powered by an LLM that pulls in relevant knowledge from the vector database.

--  &nbsp;**Automated Support Replies**  
  Incoming customer emails are classified, routed, and answered using the same knowledge base — providing friendly, branded responses without manual effort.

---

## Typical Use Cases

--  &nbsp;Streamlining customer support by handling FAQs, policies, and warranty queries automatically.  
--  &nbsp;Enabling teams to search internal knowledge bases conversationally.  
--  &nbsp;Reducing workload for support staff while ensuring consistent and accurate messaging.  
--  &nbsp;Serving as a template for enterprise RAG applications combining automation, search, and AI reasoning.  

---

## High-Level Architecture

--  &nbsp;Triggers- Google Drive (file created) + Gmail (message received)  
--  &nbsp;Ingestion- n8n Download → Default Data Loader (binary) → Recursive character text splitter → Embeddings → Pinecone addDocuments  
--  &nbsp;Index- Pinecone index (namespace per dataset, e.g., FAQ) using text-embedding-3-small (OpenAI)  
--  &nbsp;Agent- n8n AI Agent with a chat model (OpenRouter/OpenAI/etc.) + Pinecone vector store tool  
--  &nbsp;Automation- Text classifier routes emails → agent composes reply → Gmail reply node (optionally label message)  

```mermaid
flowchart TD
    A[📁 Google Drive Folder<br/>Document Storage] -->|New Document| B[🔄 Ingestion Workflow<br/>Process new files]
    
    B --> C[⚡ Text Splitter & Embeddings<br/>• Chunk text<br/>• Generate vectors]
    
    C --> D[🗃️ Pinecone Vector Database<br/>Searchable embeddings]
    
    E[💬 User Chat Query<br/>Natural language input] --> F[🤖 AI Agent<br/>Query processor]
    
    F --> D
    D --> F
    F --> G[💡 Chat Response<br/>AI-generated answer]
    
    H[📧 Incoming Email<br/>New messages] --> I[🔍 Classifier<br/>Email categorization]
    
    I -->|Customer Support| F
    F --> J[📤 Automated Reply Email<br/>AI response sent]
    
    I -->|Other| K[🚫 Ignore / Route Elsewhere<br/>Non-support handling]
    
    style A fill:#4285f4,color:#fff
    style B fill:#34a853,color:#fff
    style C fill:#ea4335,color:#fff
    style D fill:#9c27b0,color:#fff
    style E fill:#ff6d01,color:#fff
    style F fill:#f44336,color:#fff
    style G fill:#2196f3,color:#fff
    style H fill:#607d8b,color:#fff
    style I fill:#795548,color:#fff
    style J fill:#4caf50,color:#fff
    style K fill:#9e9e9e,color:#fff

