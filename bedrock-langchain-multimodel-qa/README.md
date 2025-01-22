## Project: Bedrock LangChain Multimodel Q&A and Stable Diffusion

This project demonstrates the power and versatility of AWS Bedrock by showcasing two distinct applications: a multi-model question-answering system over PDF documents and an image generation tool. It also includes individual scripts for directly interacting with specific LLMs.

*   **app.py:** Creates a Streamlit web application that allows users to ask questions about PDF documents. This application leverages LangChain to orchestrate interactions with multiple foundation models (LLMs) like Claude and Llama2, providing a rich and interactive Q&A experience.
*   **stablediffusion.py:** Generates images from text prompts using a Stable Diffusion model hosted on Bedrock. This demonstrates Bedrock's capability to run powerful generative AI models for creative tasks.
*   **claude.py:** Provides a direct interface to the Claude LLM on Bedrock, generating text in response to a prompt designed to mimic the writing style of Andrew Ng, a prominent figure in AI.
*   **llama2.py:** Similar to `claude.py`, this script provides a direct interface to the Llama 2 LLM on Bedrock, also with a prompt designed to emulate Andrew Ng's style. This highlights the differences in output and interaction patterns between different LLMs.

**Key Technologies:**

*   AWS Bedrock ☁️: Provides access to various foundation models, simplifying their integration into applications.
*   `boto3` (all scripts): The AWS SDK for Python, used for interacting with AWS services, including Bedrock.
*   `json` (all scripts): Python library for working with JSON data, used for structuring requests and parsing responses from Bedrock.

**Specific Technologies (Depending on the Script):**

*   **app.py:**
    *   LangChain 🔗: Simplifies LLM application development by providing abstractions for chains, prompts, and other components.
    *   Streamlit 🖥️: Creates an interactive web interface for the Q&A application, making it easy for users to interact with the LLMs.
    *   Titan Embeddings: Generates text embeddings, crucial for semantic search and retrieval of relevant context from the PDF documents.
    *   FAISS: A library for efficient similarity search and clustering of dense vectors, used here to store and retrieve document embeddings.
    *   PyPDF2: A library for working with PDF documents.
*   **stablediffusion.py:**
    *   Stable Diffusion XL: A powerful deep learning model for generating high-quality images from text descriptions.
*   **claude.py:**
    *   ai21.j2-mid-v1 Model: The specific Claude LLM used for text generation.
*   **llama2.py:**
    *   meta.llama2-70b-chat-v1 Model: The specific Llama 2 LLM used for text generation.

**app.py: Multi-Model Question Answering 💬**

This script creates a Streamlit web application that allows users to ask questions about PDF documents.

**Workflow:**

1.  Data Ingestion: Loads PDF documents using `PyPDFDirectoryLoader` and splits them into text chunks using `RecursiveCharacterTextSplitter`.
2.  Vector Embedding & Storage: Creates embeddings using Titan via `BedrockEmbeddings` and stores them in a FAISS vector store.
3.  Question Answering:
    *   User asks a question via the Streamlit interface.
    *   The question is embedded using Titan.
    *   Relevant text chunks are retrieved from the FAISS vector store based on embedding similarity.
    *   A prompt is constructed containing the retrieved context and the user's question.
    *   The prompt is sent to the chosen LLM (Claude or Llama2) via `Bedrock`.
    *   The LLM generates an answer, which is displayed in the Streamlit app.

**Key Functions:**

*   `data_ingestion()`: Loads and splits PDFs.
*   `get_vector_store()`: Creates/loads the FAISS vector store.
*   `get_claude_llm()`/`get_llama2_llm()`: Creates Bedrock LLM clients.
*   `get_response_llm()`: Performs retrieval and question answering.
*   `main()`: Sets up the Streamlit app.

**stablediffusion.py: Image Generation 🖼️**

This script generates images from text prompts using Stable Diffusion XL.

**Workflow:**

1.  Prompt Definition: Defines the text prompt.
2.  Payload Creation: Constructs a payload with prompt and generation parameters (e.g., `cfg_scale`, `seed`, `steps`, `width`, `height`).
3.  Model Invocation: Sends the payload to Stable Diffusion XL on Bedrock using `bedrock.invoke_model()`.
4.  Image Decoding & Saving: Decodes the base64 encoded image data and saves it as a PNG file in the `output` directory.

**Key Components:**

*   `prompt_data`: The text prompt.
*   `payload`: Generation parameters.
*   `bedrock.invoke_model()`: Sends the request to Bedrock.
*   `base64.b64decode()`: Decodes the image data.

**claude.py: Text Generation (Mimicking Andrew Ng) ✍️**

This script uses the Claude LLM to generate text in the style of Andrew Ng.

**Workflow:**

1.  Prompt Definition: Defines a prompt for Claude.
2.  Payload Creation: Creates a payload with prompt and parameters (e.g., `maxTokens`, `temperature`, `topP`).
3.  Model Invocation: Sends the payload to Claude on Bedrock.
4.  Response Processing: Extracts and prints the generated text.

**Key Components:**

*   `prompt_data`: The prompt for Claude.
*   `payload`: Generation parameters for Claude.
*   `bedrock.invoke_model()`: Sends the request to Bedrock.

**llama2.py: Text Generation (Mimicking Andrew Ng) 🦙**

This script is similar to `claude.py`, but uses the Llama 2 LLM.

**Key Differences from `claude.py`:**

*   Prompt Formatting: The prompt is wrapped in `[INST]` and `[/INST]` tags, which is the expected format for Llama 2 chat models.
*   Payload Parameters: Uses `max_gen_len`, `temperature`, and `top_p`.
*   Response Extraction: Extracts text from the `generation` field of the response.

**Key Components:**

*   `prompt_data`: The prompt for Llama 2.
*   `payload`: Generation parameters for Llama 2.
*   `[INST]` and `[/INST]` tags: Prompt formatting.
*   `bedrock.invoke_model()`: Sends the request to Bedrock.

**Running the Applications:**

**Requirements:**

A `requirements.txt` file is included with the following dependencies:

*    boto3
*    awscli
*    langchain
*    streamlit
*    faiss-cpu
*    PyPDF2

**To install the dependencies, run:**

    ```bash
    pip install -r requirements.txt
    ```

**AWS Configuration:**

* Ensure you have configured your AWS credentials correctly. The easiest way is to configure the AWS CLI: aws configure

* Running the Scripts:

* For app.py:

*    1. Place your PDF files in a directory named data in the same directory as app.py.
*    2. Run the app: streamlit run app.py

* For stablediffusion.py, claude.py, and llama2.py:

*    1. Run the specific script using python <script_name>.py