Recruitment Agent – n8n AI Workflow








An AI-powered automated recruitment assistant built with n8n that screens resumes automatically.

The workflow retrieves resumes from Gmail, extracts and analyzes the candidate’s information, compares it against a job description, evaluates strengths and weaknesses using AI, assigns a suitability score, and stores the results in Google Sheets.

This project demonstrates how workflow automation + AI agents can streamline candidate screening and reduce manual hiring effort.

Features

Automated resume ingestion from Gmail
Support for PDF and Word resumes
Automatic text extraction from documents
AI-powered candidate evaluation
Strengths and weaknesses analysis
Suitability scoring and ranking
Structured candidate database in Google Sheets
Modular workflow with reusable subflows

Workflow Architecture

The recruitment system is implemented as a modular n8n workflow composed of a main pipeline and document processing subflows.

Processing Pipeline
Gmail Trigger
      │
      ▼
Upload File (Google Drive)
      │
      ▼
File Type Switch
 ┌───────────────┐
 ▼               ▼
PDF Handler   Word Handler
 └───────┬───────┘
         ▼
     Standardize
         ▼
Download Job Description
         ▼
Extract Job Description Text
         ▼
AI Candidate Evaluation
         ▼
Structured Information Extractor
         ▼
Append Results → Google Sheets
Workflow Diagram

(Insert your workflow screenshot here)

Example:

/docs/workflow.png
System Components
1. Gmail Trigger

Monitors incoming emails and detects new resumes automatically.

Input

Email attachment (PDF or DOCX resume)

Output

Resume file

Email metadata

2. File Upload

Uploads the resume to Google Drive to maintain centralized file storage.

Output

File ID

Download link

3. File Type Detection

A Switch node identifies the file format.

Supported formats:

PDF

DOCX

The workflow then routes the file to the appropriate processing subflow.

Subflows
PDF Handler

Handles resumes submitted in PDF format.

Steps:

Download PDF

Extract text from document

Return parsed text to main workflow

Input

PDF Resume

Output

Extracted Resume Text
Word Handler

Handles resumes submitted in DOCX format.

Steps:

Download Word file

Extract document content

Return parsed text

Input

DOCX Resume

Output

Extracted Resume Text
Resume Processing
Standardization Stage

The extracted resume content is cleaned and formatted to create a consistent structure for AI analysis.

Operations include:

Remove formatting noise

Normalize text

Prepare structured input

Output

Standardized Resume Text
Job Description Processing

The workflow retrieves a job description document stored in Google Drive.

Steps:

Download job description

Extract text from the PDF

Provide text to the AI agent for comparison

AI Candidate Evaluation

The system uses Google Gemini AI to evaluate the candidate.

AI Tasks

The model performs:

Skill matching

Experience comparison

Strength identification

Weakness detection

Job suitability analysis

Candidate scoring

Example Output
Candidate: John Doe

Strengths:
- Strong Python background
- Experience with cloud platforms

Weaknesses:
- Limited leadership experience
- No exposure to Kubernetes

Suitability Score: 7.5 / 10
Recommendation: Consider for technical interview
Structured Information Extraction

The AI output is converted into structured data using a Structured Output Parser.

Extracted Fields

Candidate Name

Key Skills

Strengths

Weaknesses

Experience Summary

Suitability Score

Hiring Recommendation

Data Storage

Results are automatically stored in Google Sheets.

Example spreadsheet structure:

Candidate	Skills	Strengths	Weaknesses	Score	Recommendation
John Doe	Python, AWS	Strong backend	Limited leadership	7.5	Interview

This allows recruiters to easily filter, rank, and review candidates.

Inputs

The workflow expects:

1. Resume

Format: PDF or DOCX

Source: Gmail attachment

2. Job Description

Format: PDF

Location: Google Drive

3. Output Storage

Google Sheets document

Outputs

The system generates:

AI candidate evaluation

Resume analysis report

Suitability score

Structured spreadsheet database

Tech Stack

Automation

n8n

AI

Google Gemini Chat Model

Integrations

Gmail API

Google Drive API

Google Sheets API

Document Processing

PDF extraction

DOCX parsing
