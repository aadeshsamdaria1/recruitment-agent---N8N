Recruitment Agent – n8n AI Workflow

An AI-powered automated recruitment assistant built with n8n that screens resumes automatically.

The workflow retrieves resumes from Gmail, extracts and analyzes candidate information, compares it against a job description, evaluates strengths and weaknesses using AI, assigns a suitability score, and stores the results in Google Sheets.

This project demonstrates how workflow automation + AI agents can streamline candidate screening and reduce manual hiring effort.

🚀 Features

Automated resume ingestion from Gmail

Support for PDF and Word resumes

Automatic text extraction from documents

AI-powered candidate evaluation

Strengths and weaknesses analysis

Suitability scoring and ranking

Structured candidate database in Google Sheets

Modular workflow with reusable subflows

🏗 Workflow Architecture

The recruitment system is implemented as a modular n8n workflow with a main pipeline and document processing subflows.

<details> <summary>Click to expand the main processing pipeline</summary>
Workflow Diagram Placeholder:
/docs/workflow.png

</details>
⚙️ System Components
<details> <summary>Gmail Trigger</summary>

Monitors incoming emails and detects new resumes automatically.

Input: Email attachment (PDF or DOCX resume)
Output:

Resume file

Email metadata

</details> <details> <summary>File Upload</summary>

Uploads the resume to Google Drive to maintain centralized file storage.

Output:

File ID

Download link

</details> <details> <summary>File Type Detection</summary>

A Switch node identifies the file format.

Supported formats:

PDF

DOCX

The workflow routes the file to the appropriate processing subflow.

</details>
🗂 Subflows
<details> <summary>PDF Handler</summary>

Handles resumes submitted in PDF format.

Steps:

Download PDF

Extract text from document

Return parsed text to main workflow

Input: PDF Resume
Output: Extracted Resume Text

</details> <details> <summary>Word Handler</summary>

Handles resumes submitted in DOCX format.

Steps:

Download Word file

Extract document content

Return parsed text

Input: DOCX Resume
Output: Extracted Resume Text

</details>
📝 Resume Processing
<details> <summary>Standardization Stage</summary>

Cleans and formats the extracted resume content to create a consistent structure for AI analysis.

Operations:

Remove formatting noise

Normalize text

Prepare structured input

Output: Standardized Resume Text

</details> <details> <summary>Job Description Processing</summary>

Retrieves and processes the job description from Google Drive.

Steps:

Download job description

Extract text from PDF

Provide text to the AI agent for comparison

</details> <details> <summary>AI Candidate Evaluation</summary>

Uses Google Gemini AI to evaluate candidates.

Tasks:

Skill matching

Experience comparison

Strength identification

Weakness detection

Job suitability analysis

Candidate scoring

Example Output:

Candidate: John Doe

Strengths:
- Strong Python background
- Experience with cloud platforms

Weaknesses:
- Limited leadership experience
- No exposure to Kubernetes

Suitability Score: 7.5 / 10
Recommendation: Consider for technical interview
</details> <details> <summary>Structured Information Extraction</summary>

Converts AI output into structured data using a Structured Output Parser.

Extracted Fields:

Candidate Name

Key Skills

Strengths

Weaknesses

Experience Summary

Suitability Score

Hiring Recommendation

</details>
💾 Data Storage

Results are automatically stored in Google Sheets.

Example Spreadsheet Structure:

Candidate	Skills	Strengths	Weaknesses	Score	Recommendation
John Doe	Python, AWS	Strong backend	Limited leadership	7.5	Interview
📥 Inputs

Resume – PDF or DOCX (from Gmail attachment)

Job Description – PDF (from Google Drive)

Output Storage – Google Sheets

📤 Outputs

AI candidate evaluation

Resume analysis report

Suitability score

Structured spreadsheet database

🛠 Tech Stack

Automation: n8n
AI: Google Gemini Chat Model

Integrations:

Gmail API

Google Drive API

Google Sheets API

Document Processing:

PDF extraction

DOCX parsing
