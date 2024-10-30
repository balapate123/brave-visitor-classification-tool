
# Brave Visitor Classification Tool

A web application that classifies website visitors based on the content of a given URL, dynamically generating relevant questions to gather insights into visitors' interests and preferences.

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Setup and Installation](#setup-and-installation)
- [Deployment](#deployment)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

The **Brave Visitor Classification Tool** is designed to help website owners classify visitors into specific interest categories based on website content. The app uses a backend API for web scraping, classification, and storing responses in DynamoDB, while the frontend allows users to input URLs and answer dynamically generated questions.

## Features

- **URL-based Classification**: Accepts a URL input and scrapes content to categorize the website’s focus.
- **Dynamic Question Generation**: Based on classifications, generates questions tailored to visitor interests.
- **Answer Collection and Storage**: Collects and saves responses in a DynamoDB database.
- **Frontend and Backend Separation**: Uses React for the frontend hosted on S3 and Flask for the backend hosted on EC2.

## Tech Stack

- **Frontend**: React, Redux, CSS
- **Backend**: Python, Flask
- **Database**: AWS DynamoDB
- **Hosting**: 
  - Frontend on AWS S3 (optionally served via CloudFront)
  - Backend on AWS EC2

## Setup and Installation

### Prerequisites

- Node.js and npm
- Python 3 and pip
- AWS CLI configured with appropriate IAM permissions

### 1. Clone the Repository

```bash
git clone https://github.com/balapate123/brave-visitor-classification-tool.git
cd brave-visitor-classification-tool
```

### 2. Backend Setup

1. Navigate to the backend folder:

   ```bash
   cd visitor-classification-backend
   ```

2. Set up a virtual environment:

   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Configure AWS credentials for DynamoDB access (use IAM role on EC2 or `aws configure`).

5. Run the backend server locally (for testing):

   ```bash
   flask run --host=0.0.0.0 --port=5000
   ```

### 3. Frontend Setup

1. Navigate to the frontend folder:

   ```bash
   cd visitor-classification-frontend
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Create a `.env` file with the API URL:

   ```plaintext
   REACT_APP_API_URL=http://your-ec2-public-ip:5000
   ```

4. Build the React app:

   ```bash
   npm run build
   ```

5. Upload the `build` folder contents to S3 for hosting.

## Deployment

### Backend Deployment on EC2

1. Launch an EC2 instance and SSH into it.
2. Set up the backend project as described in **Backend Setup** above.
3. Run the backend server using `gunicorn` or configure it with an Nginx proxy for production use.

### Frontend Deployment on S3

1. In the S3 Console, create a new bucket for static website hosting.
2. Upload the contents of the `build` folder to the bucket.
3. Enable public access and static website hosting in bucket settings.
4. Optionally, configure CloudFront for HTTPS and caching.

## Usage

1. Access the frontend through the S3 or CloudFront URL.
2. Input a URL in the text field and click **Classify**.
3. Answer the generated questions and submit responses.
4. Results and responses are stored in DynamoDB for analysis.

## Project Structure

```
brave-visitor-classification-tool/
│
├── visitor-classification-backend/        # Backend (Flask) code
│   ├── app/
│   │   ├── __init__.py                    # Flask app initialization
│   │   ├── db.py                          # DynamoDB connection and functions
│   │   ├── routes.py                      # API routes
│   │   └── scraper.py                     # Web scraping logic
│   ├── run.py                             # Backend entry point
│   └── requirements.txt                   # Backend dependencies
│
└── visitor-classification-frontend/       # Frontend (React) code
    ├── public/
    ├── src/
    │   ├── redux/                         # Redux actions and reducers
    │   ├── components/                    # UI components
    │   ├── App.js                         # Main App component
    │   └── App.css                        # Main App styling
    ├── .env                               # Environment variables
    ├── package.json                       # Frontend dependencies
    └── build/                             # Build folder for deployment
```

## Contributing

Contributions are welcome! Please open an issue or create a pull request with any updates or suggestions.

## License

This project is licensed under the MIT License.

---

