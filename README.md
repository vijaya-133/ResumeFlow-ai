# ResumeFlow AI

**ResumeFlow AI** is a cloud-native web application that acts as a personal AI career coach. It leverages Google's Gemini generative model to analyze resumes against job descriptions, providing targeted feedback, a match score, and a tailored cover letter—all in a matter of seconds.

This project is designed to be a scalable, cost-effective, and powerful tool for any job seeker looking to streamline and improve their application process.


---

## Features

-   **AI-Powered Analysis:** Submits a user's resume and a target job description to the Gemini API for deep analysis.
-   **Match Score:** Generates a score from 1-10, giving a quick quantitative measure of resume alignment.
-   **Actionable Feedback:** Provides specific, actionable suggestions on how to improve the resume for the target role.
-   **Cover Letter Generation:** Automatically drafts a professional, three-paragraph cover letter tailored to the job.
-   **Serverless & Scalable:** Built on Google Cloud Run, allowing it to scale to zero (costing nothing) and handle high traffic on demand.
-   **Containerized:** A fully containerized application using Docker for consistency across development and production environments.

---

## Technology Stack

-   **Backend:** Python 3.9+ with Flask
-   **AI Model:** Google Gemini (via Vertex AI API)
-   **Cloud Platform:** Google Cloud
    -   **Compute:** Cloud Run (Serverless)
    -   **Containerization:** Cloud Build & Artifact Registry
-   **Infrastructure as Code:** Docker (`Dockerfile`)

---

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

-   Python 3.9+
-   [Google Cloud SDK](https://cloud.google.com/sdk/docs/install) installed and authenticated (`gcloud init`)
-   A Google Cloud Project with the Vertex AI API enabled and a billing account attached.
-   Docker installed (for local container testing).

### Local Development (No Docker)

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/resumeflow-ai.git
    cd resumeflow-ai
    ```

2.  **Set up a virtual environment:**
    ```bash
    python3 -m venv venv
    source venv/bin/activate
    ```

3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Authenticate with Google Cloud:**
    ```bash
    gcloud auth application-default login
    ```

5.  **Run the Flask application:**
    The application will start on `http://127.0.0.1:8080`.
    ```bash
    python app.py
    ```

6.  **Test the endpoint:**
    In a new terminal, use `curl` to send a request. Make sure you have a `test_payload.json` file in the root directory.
    ```bash
    curl -X POST \
         -H "Content-Type: application/json" \
         -d @test_payload.json \
         http://127.0.0.1:8080/analyze
    ```

---

## Deployment to Google Cloud Run

This project is designed to be deployed directly from source to Cloud Run.

1.  **Set your Google Cloud Project ID:**
    ```bash
    gcloud config set project [YOUR_PROJECT_ID]
    ```

2.  **Deploy the service:**
    Run the following command from the root of the project directory. This will use Cloud Build to containerize your application and deploy it to Cloud Run.
    ```bash
    gcloud run deploy resumeflow-ai-service \
      --source . \
      --platform managed \
      --region us-central1 \
      --allow-unauthenticated
    ```
    The command will output a **Service URL** upon successful deployment.

---

## API Endpoint

### `/analyze`

-   **Method:** `POST`
-   **Description:** Analyzes a resume and job description.
-   **Body (raw JSON):**
    ```json
    {
      "resume": "Text content of the resume...",
      "job_description": "Text content of the job description..."
    }
    ```
-   **Success Response (`200 OK`):**
    ```json
    {
      "matchScore": 8.5,
      "scoreJustification": "...",
      "resumeFeedback": [
        {
          "area": "...",
          "suggestion": "...",
          "before": "...",
          "after": "..."
        }
      ],
      "generatedCoverLetter": "..."
    }
    ```

---

## Author

-   **Vijaya** - https://www.linkedin.com/in/vijaya-k-1408bb1a8/
