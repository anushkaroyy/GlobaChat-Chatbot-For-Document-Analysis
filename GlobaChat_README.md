# GlobaChat — LLM-Powered Document Intelligence Chatbot

A full-stack document intelligence platform built for GlobaTech to automate extraction, summarisation, and Q&A over large-scale PDF documents using a large language model pipeline deployed on Google Cloud Platform.

---

## Overview

Organisations handling large volumes of PDF documents face a time-consuming challenge: manually sifting through pages to extract key information. GlobaChat addresses this by automating the entire pipeline — from PDF ingestion to structured data extraction, visualisation generation, and natural language Q&A — using an open-source LLM.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language Model | DeepSeek-R1-Distill-Qwen-15B |
| ML Framework | PyTorch, Hugging Face Transformers |
| Cloud Storage | Google Cloud Platform (GCP Buckets) |
| Backend | Python |
| PDF Processing | PyMuPDF (fitz) |
| Visualisation | Matplotlib |
| Frontend | HTML, JavaScript |
| Auth & Access | GCP Service Account Credentials |
| Environment | Google Colab (T4 GPU, 15GB RAM) |

---

## Architecture

```
GCP Bucket (PDF Input)
        |
        v
DeepSeek-R1 Pipeline (PyTorch + Transformers)
        |
        |---> summary.txt  --------> Chatbot Interface (Q&A)
        |
        |---> csv.txt
                |
                v
            CSV File ---> Matplotlib Charts ---> GCP Bucket (Output)
```

1. PDF documents are stored in a GCP bucket and pulled to the processing environment
2. The LLM pipeline batch-processes pages, generating a structured CSV and a summary per document
3. Matplotlib generates charts and graphs from the CSV data, which are uploaded back to GCP
4. The summarised content is fed into a chatbot interface supporting dynamic natural language queries

---

## Key Features

- **Batch PDF processing** — iterates through multi-page documents in configurable page batches
- **Dual output extraction** — simultaneously generates structured CSV data and human-readable summaries
- **Automated visualisation** — produces consistent charts per document using Matplotlib
- **Natural language Q&A** — chatbot interface allows users to ask both predefined and open-ended questions over document content
- **Cloud-native storage** — all inputs and outputs managed through GCP buckets with service account authentication
- **GPU memory management** — explicit torch.cuda cache clearing between batches to handle T4 memory constraints

---

## Setup & Usage

### Prerequisites

```bash
pip install torch transformers pymupdf google-cloud-storage matplotlib
```

### Environment

- Google Colab with T4 GPU runtime recommended
- GCP service account credentials JSON required for bucket access

### Running the Pipeline

1. Upload PDF files to your GCP bucket
2. Set `pdf_filename`, `summary_output_filename`, and `csv_output_filename` in the config section
3. Add your GCP service account credentials to `credentials_info`
4. Run all cells sequentially
5. Outputs are automatically uploaded to the designated GCP bucket

---

## Challenges & Limitations

- **GPU memory** — T4 constraints required use of the distilled model variant; larger models exceeded available RAM
- **PDF formatting** — inconsistently formatted source documents required preprocessing to ensure clean text extraction
- **Context window** — very long documents required chunking; inputs exceeding the model's token limit were truncated

---

## Results

- Successfully automated extraction, summarisation, and visualisation across multi-page energy-sector PDFs
- Delivered structured CSV outputs and dynamic Q&A capability to the client team at GlobaTech
- Reduced manual document review time significantly for end users

---

## Team

Anushka Roy | Advaith Sujith | Asraa Shaikh | Rhythm Shahi
University of Wollongong in Dubai — CSCI323
