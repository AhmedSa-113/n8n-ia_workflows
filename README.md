🧾 AI Resume Parser (n8n)

An n8n workflow that automatically parses CVs sent by email and stores the extracted data as structured rows in a database. Drop a resume in the inbox, get a clean candidate record — no manual entry.

How it works

1. Gmail Trigger
Monitors an inbox and fires whenever a new email with a CV attachment (PDF) arrives.

2. Prepare Data
Extract from File pulls the raw text out of the PDF, and Edit Fields cleans and normalizes it into a single text payload for the AI step.

3. Extract Information
A Basic LLM Chain powered by Google Gemini reads the resume and extracts the candidate's details — name, contact info, work history, education, and skills. A Structured Output Parser enforces a strict JSON schema so the output is always consistent and machine-readable, regardless of how the CV was formatted.

4. Save Information
An HTTP Request node sends the parsed JSON to the target endpoint, then three parallel branches handle the repeating sections of the CV. Each branch uses Edit Fields → Split Out → Create a row, so a candidate with 4 jobs, 2 degrees, and 12 skills becomes the right number of rows in each table instead of one blob:

Why it's useful
Handles any CV layout — the LLM reads meaning, not templates
Normalizes messy resumes into a queryable candidate database
Split-out rows make filtering easy ("show me everyone who knows Python")
Fully hands-off: email in, structured data out
Stack
n8n — orchestration
Google Gemini — resume understanding
Gmail API — ingestion
Structured Output Parser — schema-validated JSON
Setup
Import the workflow JSON into your n8n instance.
Connect your Gmail and Google Gemini credentials.
Update the HTTP Request URL and the base/table IDs in the Create a row nodes.
Adjust the output schema in the Structured Output Parser if you want to capture additional fields (languages, certifications, portfolio links…).
