## 🚀 Project: Bedrock LangChain Multimodel Q&A and Stable Diffusion 🖼️

This project showcases the power and versatility of AWS Bedrock by demonstrating two distinct applications:

*   **Multi-model Question Answering over PDFs 💬:** A Streamlit web application that allows users to ask questions about PDF documents. It leverages LangChain 🔗 to interact with foundation models (LLMs) like Claude and Llama2, providing an interactive Q&A experience.
*   **Image Generation with Stable Diffusion 🖼️:** A script that generates images from text prompts using a Stable Diffusion model hosted on Bedrock.

**Additional Functionality:**

*   Separate scripts for directly interacting with specific LLMs (Claude ✍️ and Llama2 🦙) to mimic Andrew Ng's writing style.

**Key Technologies:**

*   AWS Bedrock ☁️: Provides access to various foundation models.
*   `boto3` (all scripts): Python library for interacting with AWS services.
*   `json` (all scripts): Python library for working with JSON data.

**Specific Technologies (Depending on the Script):**

*   **app.py (Q&A):**
    *   LangChain 🔗
    *   Streamlit 🖥️
    *   Titan Embeddings 🔢
    *   FAISS
    *   PyPDF2
*   **stablediffusion.py (Image Generation):**
    *   Stable Diffusion XL 🎨

**Running the Applications:**

See the individual script READMEs for detailed instructions on requirements, setup, and usage.

**AWS Configuration:**

Ensure you have configured your AWS credentials correctly using the AWS CLI: `aws configure`

**Further Exploration:**

Refer to the individual script READMEs (`app.py`, `stablediffusion.py`, `claude.py`, `llama2.py`) for comprehensive explanations, workflow breakdowns, and code details.