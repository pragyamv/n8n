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
    A[Google Drive Folder] -->|New Document| B[Ingestion Workflow]
    B --> C[Text Splitter & Embeddings]
    C --> D[Pinecone Vector Database]

    E[User Chat Query] --> F[AI Agent]
    F --> D
    D --> F
    F --> G[Chat Response]

    H[Incoming Email] --> I[Classifier]
    I -->|Customer Support| F
    F --> J[Automated Reply Email]
    I -->|Other| K[Ignore / Route Elsewhere]

