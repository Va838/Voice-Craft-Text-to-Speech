# Voice-Craft-Text-to-Speech
# 🗣️ AWS Serverless Text-to-Speech Web Application using Amazon Polly

This project is a **serverless web application** that converts user-submitted text into speech using **Amazon Polly**. Built with fully managed AWS services, the application provides an interactive web interface for users to select a voice, enter text, and receive an audio file (MP3) generated in real-time.

---

## 📐 Architecture Overview

![Screenshot 2025-06-26 154942](https://github.com/user-attachments/assets/f2ec4dab-b26b-40a7-99dd-fc02b1ef9e13)


### 🔧 Components

#### 🔹 Frontend
- `index.html` – Web interface for user interaction.
- `styles.css` – Styling for a clean UI.
- `scripts.js` – JavaScript logic for sending/receiving data via API Gateway.

#### 🔹 Backend (AWS Serverless Stack)
- **API Gateway** – Exposes REST endpoints to the frontend.
- **AWS Lambda Functions**:
  - `add_new_posts.py` – Accepts text input, saves to DynamoDB, and triggers SNS.
  - `convert_text_to_audio.py` – Invoked by SNS, reads text from DB, uses Polly to convert, saves MP3 in S3, updates DB with audio URL.
  - `read_table_items.py` – Fetches all items from DynamoDB for frontend display.
- **Amazon DynamoDB** – Stores:
  - User input text
  - Selected voice
  - Status (`PENDING`, `COMPLETED`)
  - MP3 audio file URL
- **Amazon SNS** – Triggers the audio conversion Lambda asynchronously.
- **Amazon Polly** – Synthesizes speech from text.
- **Amazon S3** – Stores and serves public MP3 files.

---

### Backend Deployment

Deploy the following AWS resources manually or using tools like SAM / Terraform:

- **DynamoDB Table**
- **S3 Bucket**
- **SNS Topic**
- **API Gateway Endpoints**
- **Lambda Functions**:
  - `add_new_posts.py`
  - `convert_text_to_audio.py`
  - `read_table_items.py`

## 📁 File Structure

```
project-root/
│
├── Voice Craft/
│   ├── index.html
│   ├── styles.css
│   ├── scripts.js
│   └── error.html
│
├── add_new_posts.py             # Lambda function: handle new submissions
├── convert_text_to_audio.py     # Lambda function: convert text to speech
├── read_table_items.py          # Lambda function: fetch all items
├── arc_diagram                  # Architecture image (optional)
└── README.md                    # Project documentation
```

---

## 📌 Important Points

- All AWS resources should be created in the **us-east-1** region.
- This app is intended for educational and demonstration purposes.
- Be mindful of **Amazon Polly quotas and costs** during heavy usage.






