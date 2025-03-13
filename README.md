# **Betty Neels Generative AI Model**

## **Overview**
This project is a **Retrieval-Augmented Generation (RAG) NLP model** designed to generate romance novels in the style of **Betty Neels**. The model is built using **LLaMA 2** and leverages a collection of **28 Betty Neels novels** stored in a vector database for context retrieval. By combining **structured prompting, embedding retrieval, and generative modeling**, the system produces novel chapters that closely mimic Neels' unique storytelling style.

## **Workflow**
### **1. PDF Preprocessing (Extract & Clean Text)**
- **Convert PDFs to Text:**
  - Utilize `PyMuPDF` or `pdfplumber` to extract raw text from the novels.
- **Clean & Structure the Text:**
  - Remove **headers, footers, and page numbers**.
  - Split text into chapters or meaningful chunks (~**About 2500 tokens** per chunk).
  - Convert text into structured formats such as **JSON, Markdown, or plain text**.
- **Tokenization for Embeddings:**
  - Use a tokenizer (e.g., `sentence-transformers` or `tiktoken`) to ensure proper chunking for embeddings.

### **2. Storing Data in a Vector Database (ChromaDB)**
- **Select an Embedding Model:**
  - OpenAI’s `text-embedding-ada-002` (**API-based**) or a local model like `sentence-transformers` (`all-MiniLM-L6-v2`).
- **Generate & Store Embeddings:**
  - Convert text chunks into **dense vectors**.
  - Store embeddings efficiently in **ChromaDB**.
- **Metadata Storage:**
  - Maintain metadata such as **chapter titles, book names, and page numbers** for context retrieval.

### **3. Structured Prompting & Querying the Database**
- **User Input:**
  - Model receives **structured prompts** (e.g., _"Write a chapter in Betty Neels’ style about a nurse meeting a wealthy doctor in Holland."_).
- **Search Vector Database:**
  - Convert the user’s input into an **embedding**.
  - Retrieve the **top-k most relevant passages** from the vector database.
- **Construct a Contextual Prompt:**
  - Use retrieved passages to enhance **prompt formulation via in-context learning (ICL)**.

### **4. Generative Model (LLaMA 2) for Novel Writing**
- **Model Selection:**
  - Utilize **LLaMA 2 (7B or 13B)** with fine-tuning for stylistic improvements.
- **Generation Process:**
  - Feed the **structured prompt** into **LLaMA 2**.
  - Use **temperature and top-k sampling** to balance creativity and coherence.
- **Iterative Refinement:**
  - Generate chapters **iteratively** instead of producing an entire novel at once.
  - Apply a **feedback loop** (human review or AI-based ranking for quality control).

### **5. Post-Processing & Compilation**
- **Edit & Refine Text:**
  - Apply **post-processing techniques** for coherence (**AI-assisted editing optional**).
- **Compile Full Novel:**
  - Merge generated chapters into a **complete novel format**.
- **Output Formats:**
  - Export final novels in **PDF, EPUB, or DOCX** for readability and distribution.

## **Tech Stack**
- **PDF Processing:** `PyMuPDF`
- **Vector Database:** `ChromaDB`
- **Embeddings:** `sentence-transformers`, OpenAI API (`text-embedding-ada-002`)
- **LLM:** `LLaMA 2`

## **Future Updates**
- Find and collect more publically available texts to increase data.
- Fine-tune LLaMA 2 further with Neels' text for better stylistic accuracy.
- Enhance metadata tagging for improved retrieval precision.
- Expand the prompt engineering module to support dynamic storytelling.
