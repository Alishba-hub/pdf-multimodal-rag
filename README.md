# PDF Multimodal RAG (Colab Edition)

A **Colab-ready Python pipeline** to extract images from PDFs, generate embeddings using **Voyage AI** and **CLIP**, and perform **multimodal vector search** with MongoDB. Ideal for research document understanding, summarization, and retrieval.

---

## Features

- **PDF to Image Extraction** – Convert every page of a PDF into high-resolution images.  
- **Multimodal Embeddings** – Generate embeddings for images using **Voyage AI** and **CLIP**.  
- **Vector Search** – Perform semantic search over PDF pages using MongoDB’s vector search.  
- **MongoDB Integration** – Store images, embeddings, and metadata efficiently.  
- **Colab-Optimized** – Run directly on Google Colab without local setup.

---

## How to Use in Colab

### 1. Open the Notebook

- Click **Open in Colab** (if you include a link in your repo).  
- Or upload the notebook (`.ipynb`) directly to Colab.

### 2. Full Setup & Run (API keys, MongoDB, PDF processing, and vector search)

```python
# -----------------------------
# 1. Install dependencies
# -----------------------------
!pip install pymupdf pymongo voyageai sentence-transformers pillow tqdm

# -----------------------------
# 2. Set API Keys
# -----------------------------
import getpass
import os

# Set Voyage AI API key
os.environ["VOYAGE_API_KEY"] = getpass.getpass("Enter your Voyage AI API key: ")

# Set Gemini API key
GEMINI_API_KEY = getpass.getpass("Enter your Gemini API key: ")

# -----------------------------
# 3. Connect to MongoDB Atlas
# -----------------------------
from pymongo import MongoClient

username = "your_username"
password = "your_password"
MONGODB_URI = f"mongodb+srv://{username}:{password}@clustername.mongodb.net/?retryWrites=true&w=majority"

client = MongoClient(MONGODB_URI)
db = client["mongo_rag_app"]
collection = db["pdf_images_embeddings"]

# -----------------------------
# 4. Clear collection (optional)
# -----------------------------
collection.delete_many({})
print("Collection cleared!")

# -----------------------------
# 5. Process PDF and upload images
# -----------------------------
process_pdf("path/to/deepseek_paper.pdf")

# -----------------------------
# 6. Perform vector search
# -----------------------------
vector_search(
    "Summarize the Pass@1 accuracy of Deepseek R1 against other models.",
    model="voyage",
    display_images=True
)
