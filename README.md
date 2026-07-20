# 📸 Automated Microstock Metadata Generation Pipeline 🚀

An automated, low-code data pipeline built in **n8n** that streamlines the workflow for microstock contributors. This workflow automatically ingests images from a designated **Google Drive** folder, uses generative AI (**Google Gemini**) to analyze the visual assets, extracts SEO-optimized commercial metadata, cleans the data via **JavaScript**, and logs everything seamlessly into **Google Sheets**.

---

## 🎯 The Problem it Solves
Managing metadata keywording for multi-media marketplaces (like Adobe Stock or Shutterstock) is tedious and time-consuming. This pipeline automates the entire asset-tagging workflow, generating high-velocity commercial titles, descriptions, and exactly 50 relevant keywords in seconds—ensuring compliance with stock platform guidelines while drastically reducing manual overhead.

## 🛠️ Tech Stack & Architecture

*   **n8n** - Workflow Orchestration & Data Pipelines 🔄
*   **Google Drive API** - Source Asset Ingestion 📁
*   **Google Gemini (LangChain Node)** - Advanced Computer Vision & AI Metadata Generation 🧠
*   **JavaScript** - Custom Regex & Text Sanitization 💻
*   **Google Sheets API** - Structured Metadata Logging 📊

---

## 📐 Workflow Architecture Diagram

The workflow follows a strict, linear batch-processing pattern to prevent data mismatching and respect API rate limits:

```text
[Manual Trigger] ➔ [Google Drive: List Folder] ➔ [Loop Over Items]
                                                          │
   ┌──────────────────────────────────────────────────────┘
   ▼
[Download File] ➔ [Gemini: Analyze Image] ➔ [JS: Clean & Structure] ➔ [Google Sheets: Log Row] ➔ (Back to Loop)
```

✨ Key Features

    ⚡ Manual Batch Processing: Triggered on-demand to scan an entire folder and cleanly iterate through all newly added images in a single run.

    🤖 Precise Prompt Engineering: Configured to enforce strict Adobe Stock compliance (e.g., descriptions under 200 characters, no redundant fluff, and high-relevancy keyword sorting).

    🧹 Smart Data Sanitization: A custom JavaScript node uses Regular Expressions (Regex) to parse Gemini's raw textual output, extract distinct fields, and strip out annoying structural line breaks before logging.

    🛡️ Built-in API Safeguards: Implements a retry-on-fail policy with controlled wait times to gracefully handle API rate limiting (429 Too Many Requests).

🚀 How to Set Up and Use
1. Prerequisites

    A running instance of n8n (Self-hosted or Cloud).

    A Google Cloud Service Account with access to the Google Drive API and Google Sheets API.

    A Google Gemini API Key.

2. Import the Workflow

    Download the workflow.json file from this repository.

    In your n8n canvas, click the menu on the top right (...) and select Import from File.

    Select the downloaded JSON file.

3. Configure Your Environment (Placeholders)

To protect sensitive credentials, all personal keys and structural IDs have been stripped from the JSON. Make sure to update the following:

    Google Drive (Search Node): Select your credentials and update the Folder filter to point to your specific input folder.

    Google Gemini Node: Link your Gemini API Account and choose your desired vision model (e.g., gemini-3.5-flash).

    Google Sheets Node: Select your credentials, paste your spreadsheet's unique Spreadsheet ID into the Document ID field, and verify your sheet name mapping.

📈 Future Enhancements

    [ ] Integrate automatic batch uploading to FTP servers for Shutterstock and Adobe Stock.

    [ ] Add an AI-driven image quality scoring gate before generating metadata.

    [ ] Implement email/Slack notifications upon batch completion.

💡 Feel free to fork this repository, open issues, or submit pull requests to improve the pipeline logic!
