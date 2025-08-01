# NotebookLM-n8n: A Multi-Agent AI System

## 📖 Overview

NotebookLM-n8n is a sophisticated, multi-agent AI framework developed entirely on the n8n automation platform. This project serves as a powerful analogue to services like Google's NotebookLM, engineered to intelligently ingest, process, comprehend, and creatively act upon unstructured data. By orchestrating a suite of specialized AI agents, the system can handle inputs from text, documents, and web content, transforming them into a structured, searchable knowledge base and generating diverse outputs like summaries, visual mindmaps, and audio podcasts.

## ✨ Core Features

-   **Multi-Modal Ingestion**: Seamlessly processes content from plain text, live website URLs, YouTube video links, and uploaded PDF documents.
-   **Intelligent Content Processing**: Leverages AI to automatically clean extraneous data, generate concise summaries, and create vector embeddings for all ingested information.
-   **Persistent Long-Term Memory**: Utilizes a Supabase PostgreSQL database with the `pgvector` extension, creating a robust and persistent vector store for long-term knowledge retention and semantic search.
-   **On-Demand Creative Generation**: Dynamically creates rich media outputs, including visually appealing mindmaps and human-like audio podcasts, based on the processed content.
-   **Conversational Q&A**: Features a Retrieval-Augmented Generation (RAG) agent that provides context-aware answers to user questions by searching its stored knowledge base.
-   **Modular and Scalable Architecture**: Built using a hub-and-spoke model, with a central `Main Workflow` orchestrating independent, specialized sub-workflows for maximum modularity and ease of maintenance.

## 🛠️ System Architecture & Workflow

The system's architecture is designed for clarity and scalability, with a central "brain" coordinating a team of "specialists."

-   **The Hub (`Main Workflow`)**: This is the central orchestrator that receives all user interactions from Telegram. It contains the primary `AI Agent`, which uses a sophisticated prompt to analyze user intent and delegate tasks to the appropriate specialist agent.
-   **The Spokes (Specialized Sub-Workflows)**: Each core function is encapsulated in a dedicated sub-workflow, which is called as a "tool" by the main agent. This separation of concerns ensures that each component is independently testable and maintainable.
    -   `Preprocessing Agent`: The data janitor. It validates and cleans all incoming data.
    -   `Summarization Agent`: The analyst. It distills cleaned text into concise summaries.
    -   `Mindmap Agent`: The visual artist. It transforms summaries into structured, colorful diagrams.
    -   `Podcast Agent`: The narrator. It converts summaries into high-quality audio files.
    -   `Storage Agent`: The librarian. It creates vector embeddings and archives knowledge in the database.
    -   `Retrieval Agent`: The researcher. It searches the database to find contextually relevant answers to user questions.

## ⚙️ Technology Stack & API Integrations

This project is a powerful demonstration of API orchestration, connecting best-in-class services to achieve its goals.

| Service | Role & Purpose |
| :--- | :--- |
| **n8n** | The core automation platform for workflow design, orchestration, and execution. |
| **Telegram** | Provides the primary user interface for all interactions. |
| **OpenRouter** | Serves as the gateway to various large language models (LLMs) for the main AI Agent's reasoning and decision-making. |
| **Cohere** | Generates the high-quality vector embeddings necessary for semantic search. |
| **Supabase** | Provides the scalable PostgreSQL database and `pgvector` extension for the system's long-term memory. |
| **ElevenLabs** | Delivers state-of-the-art, human-like text-to-speech synthesis for the podcast feature. |
| **hcti.io** | A simple API service that converts HTML and CSS code into high-quality images for the mindmap feature. |
| **Mermaid.js**| A JavaScript-based library used to render structured text into clean and consistent diagrams for mindmaps. |

## 🚀 Getting Started

### Prerequisites

To deploy and run this project, you will need the following:

1.  An active **n8n** instance (n8n.cloud is recommended for ease of use).
2.  A configured **Telegram Bot** and its API Token.
3.  Active accounts and API keys for:
    -   **OpenRouter**
    -   **Cohere**
    -   **Supabase** (Project URL and Anon Key)
    -   **ElevenLabs**
    -   **hcti.io** (User ID and API Key)
4.  A **Supabase** project with the `pgvector` extension enabled and a table configured to store content, metadata, and embeddings.

### Installation & Configuration

1.  **Import Workflows**: Download the JSON files provided for all workflows (`Main Workflow` and all agent sub-workflows).
2.  **Create Workflows in n8n**: In your n8n instance, create new workflows and import the corresponding JSON for each.
3.  **Configure Credentials**: Navigate to the "Credentials" section in your n8n settings. Add new credentials for each of the services listed in the prerequisites, pasting in your secret keys and tokens.
4.  **Link Credentials**: Open each workflow and link the relevant nodes to the credentials you just created (e.g., connect your OpenRouter credential to the `OpenRouter Chat Model` node).
5.  **Activate the `Main Workflow`**: On the `Main Workflow` canvas, toggle the "Active" switch to `on`. This will register the Telegram webhook and bring your bot online.

## 🧪 Usage Examples

Interact with the system via your configured Telegram bot.

-   **Process a Web Article**:
    `Summarize this for me: https://n8n.io/blog/`

-   **Process Text and Create a Mindmap**:
    `Create a visual diagram for this: The Industrial Revolution was the transition to new manufacturing processes in Great Britain, continental Europe, and the United States, in the period from about 1760 to sometime between 1820 and 1840.`

-   **Process a PDF and Create a Podcast**:
    *(Upload a PDF document to the chat with the caption)*: `Make a podcast of this document.`

-   **Ask a Question about Stored Content**:
    *(After processing the content above)*: `What was the time period of the Industrial Revolution?`

## 🌟 Future Development & Recommendations

-   **Enhanced Error Handling**: Implement robust error-handling branches within each sub-workflow to gracefully manage API failures and provide informative feedback to the user.
-   **Integrate General Web Search**: Add a new tool using an API like SerpApi to allow the agent to answer questions about real-time events or topics not yet in its knowledge base.
-   **Upgrade API Tiers**: For production-level applications, upgrade key services like ElevenLabs and hcti.io to paid tiers to remove free-tier limitations, increase rate limits, and remove watermarks.
-   **Advanced State Management**: For more complex, multi-turn conversations, explore using n8n's built-in memory options or an external database (like Redis) to manage conversational state more explicitly.
