# 🚀 Project Name

## 📌 Table of Contents
- [Introduction](#introduction)
- [Demo](#demo)
- [Inspiration](#inspiration)
- [What It Does](#what-it-does)
- [How We Built It](#how-we-built-it)
- [Challenges We Faced](#challenges-we-faced)
- [How to Run](#how-to-run)
- [Tech Stack](#tech-stack)
- [Team](#team)

---

## 🎯 Introduction
The Gen AI Gatekeeper is an intelligent email monitoring and processing solution designed to streamline the management of incoming emails in a shared mailbox. Leveraging advanced generative AI capabilities and seamless orchestration, it categorizes, extracts key information, and provides actionable insights from emails based on the request types that can be channeled to various Service Requests.

## 🎥 Demo
🔗 [Live Demo](#) (if applicable)  
📹 ![image](https://github.com/user-attachments/assets/c8662324-ccd8-4ecc-90cd-85021929206d)
 
🖼️ Screenshots:

![image](https://github.com/user-attachments/assets/339e786e-4636-45c4-a18f-ccfaaafe935d)

PPTX:
The ppt is uploaded to the artifacts folder

## 💡 Inspiration
Shared mailboxes are often inundated with emails from various senders, making it challenging for teams to prioritize and process requests efficiently. Manual sorting and data extraction are time-consuming and prone to errors. Inspired by the power of generative AI and efficient orchestration, we aimed to create a smart gatekeeper that automates email triaging, reduces human effort, and enhances decision-making with data-driven insights.

## ⚙️ What It Does
The Gen AI Gatekeeper monitors the backed up emails (.eml fomat) from a shared mailbox and processes incoming emails in a batch by:

- 🔹**Email Categorization:** Extracts and interprets email content and attachments to categorize emails into predefined "Request Type" (e.g., Adjustment, AUTransfer) and "Sub Request Type" (e.g., RateAdjustment, ParticipantManagement) based on sender intent, with reasoning provided and a confidence score.

- 🔹**Content-Based Data Extraction:** Identifies and extracts key attributes (e.g., Borrower Name, amount, expiration date) from email bodies and attachments for use in service requests.

- 🔹**Primary Intent Detection:** Determines the sender’s primary intent, even in emails discussing multiple topics.

- 🔹**Duplicate Detection:** Identifies and flags duplicate emails to prevent redundant processing.

- 🔹**Analytics & Insights:** Provides data on email volumes, request type distribution, and other actionable insights.

## 🛠️ How We Built It

- 🔹**Email Ingestion: **Connected to a backup folder of a shared mailbox and loaded the emails.

- 🔹**AI Processing:** Employed a fine-tuned generative AI model based on Llama3-70b-8192 and all-MiniLM-L6-v2 to analyze email content and attachments, categorize requests, and extract data.

- 🔹**Rule Engine:** Built a configurable ruleset for mapping sender intent to request types and extracting specific fields.

- 🔹**Orchestration:** Designed a workflow to seamlessly coordinate email ingestion, AI processing, and data storage.

- 🔹**Analytics Module:** Added a dashboard to visualize email trends and statistics.

- 🔹**Testing:** Validated the solution with diverse email datasets to ensure accuracy in intent detection and data extraction.

## 🚧 Challenges We Faced

- 🔹**Request Types and Sub Types Ambiguity:** One of the key challenges encountered during the development of the email classification system was ensuring that the request types and sub-request types generated by the ChatGPT model matched the predefined request types provided in the problem statement. The predefined request types were specified in a JSON file (request_types.json), and the goal was to classify emails accurately based on these types. The ChatGPT model, while powerful in generating text and understanding context, sometimes produced request types and sub-request types that did not exactly match the predefined categories. This mismatch posed several issues:

         - 🔹Inconsistent Classifications: The model occasionally generated request types that were semantically similar but not identical to the predefined types. For example, the model might classify an email as "Payment Request" instead of the predefined "Money Movement Outbound".

        - 🔹Validation Difficulties: Ensuring that the generated request types were valid and matched the predefined categories required additional validation steps. This validation was necessary to maintain consistency and accuracy in the classification results.

- 🔹**Attachment Variability:** Processing diverse attachment formats (PDFs, Word docs, images) demanded advanced parsing capabilities. 

- 🔹**Duplicate Detection:** Accurately identifying duplicates across slight variations in email content was complex. 

## 🏃 How to Run
1. Clone the repository  
   ```sh
   git clone https://github.com/ewfx/gaied-neuronauts.git
   ```
2. Install dependencies  
   ```sh
   pip install -r requirements.txt (for Python)
   ```
3. Launch the app from code > src folder using 
   ```sh
   python -m uvicorn main:app --reload
   ```
4. From postman trigger this request after running the code from Visual Studio
   ```sh
   http://localhost:8000/process-emails/?email_dir_path=<scenario single request>
   ```   
## 🏗️ Tech Stack
- 🔹 Frontend: React
- 🔹 Backend: FastAPI, Uvicorn
- 🔹 Gen AI models: Llama3-70b-8192, all-MiniLM-L6-v2

## 🏗️ Sample Output

{
    "finaloutput": [
        {
            "classification": [
                {
                    "Request_Type": "Tax Compliance and Reporting",
                    "SubRequest_Type": "Form 1098 Issuance",
                    "Confidence_Score": 1,
                    "Reasoning": "The email explicitly states that the Form 1098 is available for download and a paper copy has been mailed.",
                    "Priority": 0.5,
                    "Review": ""
                }
            ],
            "fields": [
                {
                    "request_type": "Tax Compliance and Reporting",
                    "extracted_data": {
                        "Borrower Name": "Brian Williams",
                        "Borrower Tax ID": null,
                        "Lender Name": "Loan Servicing Co.",
                        "Lender Tax ID": null,
                        "Loan/Facility ID": "#1357924",
                        "Interest Paid": "$8,423.15",
                        "Property Address": null,
                        "Tax Year": "2024",
                        "Form Issuance Date": null,
                        "Contact Information for Questions": "Tax Information Department"
                    }
                }
            ],
            "duplicates": [
                {
                    "Subject": "2024 Mortgage Interest Statement (Form 1098) Available - Loan #1357924",
                    "Duplicate_Resons": "Duplicate Found in :subject for Processed email (2024 Mortgage Interest Statement (Form 1098) Available - Loan #1357924) with Confidence score: 1.00; Duplicate Found in :sender for Processed email (2024 Mortgage Interest Statement (Form 1098) Available - Loan #1357924) with Confidence score: 1.00; Duplicate Found in :content for Processed email (2024 Mortgage Interest Statement (Form 1098) Available - Loan #1357924) with Confidence score: 1.00; Duplicate Found in :sender for Processed email (Fw: 2024 Mortgage Interest Statement (Form 1098) Available - Loan #8901234) with Confidence score: 0.91; Duplicate Found in :content for Processed email (Fw: 2024 Mortgage Interest Statement (Form 1098) Available - Loan #8901234) with Confidence score: 0.91",
                    "Verify_Reasons": false
                }
            ]
        }]}

## 👥 Team
- **Blessy Mathew M** - [GitHub](#) | [LinkedIn](#)
- **Cini Varghese** - [GitHub](#) | [LinkedIn](#)
- **Gayathri Aravind** - [GitHub](#) | [LinkedIn](#)
- **Seena Jose** - [GitHub](#) | [LinkedIn](#)
- **Purushotham Reddy Polu** - [GitHub](#) | [LinkedIn](#)
