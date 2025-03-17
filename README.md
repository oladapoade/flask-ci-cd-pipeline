# 🚀 CI/CD Pipeline for a Flask App with GitHub Actions

This project demonstrates how to create a CI/CD pipeline using GitHub Actions for a basic Flask web application. The pipeline automates environment setup, dependency installation, and testing to ensure application quality and deployment readiness.

## 📌 What I Built

- A Flask application that prints a custom message
- A GitHub Actions CI/CD pipeline triggered on code push
- Automation for:
  - Creating a Python virtual environment
  - Installing dependencies
  - Running the Flask app
  - Simulating an endpoint test using curl

## 🛠 Technologies Used

- Python 3.12  
- Flask  
- GitHub Actions  
- Bash  
- VS Code with WSL (Ubuntu)

## 🧱 Step-by-Step Implementation

Step 1: Create Project Folder  
📸 01_project_folder_created.png

Step 2: Set Up Virtual Environment  
📸 02_virtualenv_fixed_and_activated.png  
Commands used:  
sudo apt install python3.12-venv  
python3 -m venv venv  
source venv/bin/activate

Step 3: Install Flask and Create requirements.txt  
📸 03_requirements_file_created.png  
Commands:  
pip install flask  
pip freeze > requirements.txt

Step 4: Write the Flask App  
📸 04_flask_app_py_code.png  
app.py content:

from flask import Flask  
app = Flask(__name__)  

@app.route("/")  
def home():  
    return "Hello from Oladapo Cloud Solutions – CI/CD with Flask!"  

if __name__ == "__main__":  
    app.run(debug=True)

Step 5: Run and Test Flask App Locally  
📸 05_flask_app_in_browser.png  
Command: python app.py  
Verified at http://127.0.0.1:5000

Step 6: Initialize Git and Prepare for GitHub  
📸 06a_git_branch_renamed.png  
Commands:  
git init  
git branch -m main

Step 7: Create .gitignore  
📸 06b_gitignore_created.png  
Contents:  
venv/  
__pycache__/  
*.pyc

Step 8: Push Code to GitHub  
📸 13_ci_cd_push_with_token_success.png  
Command used:  
git push https://<username>:<token>@github.com/<username>/<repo>.git

## ⚙️ GitHub Actions CI/CD Workflow  
📸 15_ci_cd_workflow_code.png  
.github/workflows/ci-cd.yml content:

name: Flask CI/CD Pipeline

on:  
  push:  
    branches: [ main ]

jobs:  
  build:  
    runs-on: ubuntu-latest

    steps:  
    - name: Checkout Code  
      uses: actions/checkout@v3

    - name: Set up Python  
      uses: actions/setup-python@v4  
      with:  
        python-version: '3.12'

    - name: Install Dependencies  
      run: |  
        python -m venv venv  
        source venv/bin/activate  
        pip install -r requirements.txt

    - name: Simulate Test  
      run: |  
        echo "Simulating test step..."  
        python app.py &  
        sleep 3  
        curl http://127.0.0.1:5000

## ✅ Pipeline Running on GitHub  
📸 10_github_actions_pipeline_running.png  
Triggered automatically after pushing to GitHub.

## 🔍 Pipeline Test Output  
📸 16_ci_cd_pipeline_logs_success.png  
Output:  
Test passed – app installed successfully!  
CI/CD Pipeline successful!

## 💡 What I Learned

- Automating deployment pipelines using GitHub Actions  
- Writing workflow files in YAML  
- Testing APIs using curl inside CI/CD  
- Handling access tokens and GitHub authentication  

## 📣 Author

Oladapo Adenekan  
GitHub: https://github.com/oladapoade

## 📌 Bonus Ideas

- Add Docker + DockerHub integration  
- Add unit testing using pytest  
- Auto-deploy to AWS EC2, Heroku, or Render  

## ❗ Problems Faced & Solutions

Problem 1: Virtual environment creation failed  
Error: "The virtual environment was not created successfully because ensurepip is not available."  
✅ Solution: Installed the missing package using:  
sudo apt install python3.12-venv

---

Problem 2: App not showing up in browser  
✅ Solution: Verified Flask was installed, and visited http://127.0.0.1:5000

---

Problem 3: GitHub push failed with 403 error  
Error: "Permission to <repo> denied to oladapo2000941"  
✅ Solution: Used a personal access token and pushed manually:  
git push https://<username>:<token>@github.com/<username>/<repo>.git

---

Problem 4: Simulate Test step missing in GitHub Actions  
✅ Solution: Added the missing step to `ci-cd.yml`:

- name: Simulate Test  
  run: |  
    echo "Simulating test step..."  
    python app.py &  
    sleep 3  
    curl http://127.0.0.1:5000

---

Problem 5: Right-click not working in VS Code  
✅ Solution: Used terminal to create folders and files:  
mkdir -p .github/workflows  
touch .github/workflows/ci-cd.yml

---

Problem 6: GitHub Actions step named "Run python..."  
✅ Solution: Added `name:` field manually for better readability.

---

Problem 7: Terminal hiding files in VS Code  
✅ Solution: Temporarily closed the terminal panel to access Explorer view.

---

Problem 8: Forgot to commit README.md  
✅ Solution:  
git add README.md  
git commit -m "Added README"  
git push origin main

## ✅ Takeaway:
Each issue helped improve my problem-solving skills, Git confidence, and ability to build real-world CI/CD projects from scratch.
