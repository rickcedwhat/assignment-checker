Assignment Checker API
This project provides a FastAPI backend with two main services:

File Metadata Modifier: Allows authorized users to upload Office documents (.docx, .pptx, .xlsx) and change metadata.

Assignment Grader: Uses the Gemini Pro model to analyze an assignment against a rubric.

The API is secured using Google OAuth 2.0, requiring a valid Google ID Token for all protected endpoints.

Authentication Flow
This API does not handle the user login process. It only validates tokens. A typical workflow is:

A frontend application (e.g., a React or Vue app) implements a "Sign in with Google" button.

After the user signs in, the frontend receives a unique ID Token (a JWT) from Google.

The frontend makes requests to this API, including the token in the Authorization header: Authorization: Bearer <ID_TOKEN>.

This FastAPI backend verifies the token with Google's servers. If valid, it processes the request.

Local Setup & Running
1. Prerequisites
Python 3.8+

A Google Cloud Platform project.

2. Get Your Google Client ID
Before running the app, you need to configure Google Sign-In.

Go to the Google Cloud Console.

Select your project.

Navigate to APIs & Services -> Credentials.

Click + CREATE CREDENTIALS and select OAuth client ID.

Choose Web application as the application type.

Give it a name (e.g., "Assignment Checker API Client").

Under Authorized JavaScript origins, add http://localhost:8000 for local testing.

Click CREATE. You will be shown your Client ID. Copy this value.

3. Installation
Clone the repository and install the required packages:

git clone <your-repo-url>
cd <your-repo-directory>
pip install -r requirements.txt

4. Environment Variables
Create a .env file in the root directory.

# .env file
GOOGLE_CLIENT_ID="your-google-client-id-goes-here"
GOOGLE_API_KEY="your-google-ai-studio-api-key"

Replace "your-google-client-id-goes-here" with the Client ID you got from the Google Cloud Console.

Replace "your-google-ai-studio-api-key" with your Gemini API key.

5. Running the Application
Start the local development server:

uvicorn main:app --reload

The API will be available at http://127.0.0.1:8000. You can access the interactive documentation at http://127.0.0.1:8000/docs.

Note: To test the protected endpoints in the docs, you'll need to get a valid ID token from a frontend application and paste it into the authorization modal.

Deployment to Railway
Prepare Your Project: Commit your updated main.py and requirements.txt to GitHub.

Configure Railway: In your Railway project, go to the "Variables" tab.

Remove the old SERVICE_API_KEY variable if it exists.

Add GOOGLE_CLIENT_ID and paste your client ID.

Ensure GOOGLE_API_KEY is set correctly.

Update OAuth Origins: In your Google Cloud Console Credentials page, add your Railway app's public URL (e.g., https://your-app-name.up.railway.app) to the list of Authorized JavaScript origins. This is crucial for it to work once deployed.