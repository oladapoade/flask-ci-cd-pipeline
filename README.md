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

### Step 1: Create Project Folder  
![Step 1](01_project_folder_created.png)

### Step 2: Set Up Virtual Environment  
![Step 2](02_virtualenv_fixed_and_activated.png)

```bash
sudo apt install python3.12-venv
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Flask and Create requirements.txt  
![Step 3](03_requirements_file_created.png)

```bash
pip install flask
pip freeze > requirements.txt
```

### Step 4: Write the Flask App  
![Step 4](04_flask_app_py_code.png)

```python
from flask import Flask  
app = Flask(__name__)  

@app.route("/")  
def home():  
    return "Hello from Oladapo Cloud Solutions – CI/CD with Flask!"  

if __name__ == "__main__":  
    app.run(debug=True)
```

### Step 5: Run and Test Flask App Locally  
![Step 5](05_flask_app_in_browser.png)

```bash
python app.py
```

Visit: http://127.0.0.1:5000

### Step 6a: Initialize Git  
![Step 6a](06a_git_branch_renamed.png)

```bash
git init
git branch -m main
```

### Step 6b: Create .gitignore  
![Step 6b](06b_gitignore_created.png)

```
venv/
__pycache__/
*.pyc
```

### Step 8: Push Code to GitHub  
![Step 8](13_ci_cd_push_with_token_success.png)

```bash
git push https://<username>:<token>@github.com/<username>/<repo>.git
```

## ⚙️ GitHub Actions CI/CD Workflow  
![Workflow](15_ci_cd_workflow_code.png)

```yaml
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
```

## ✅ Pipeline Running on GitHub  
![Pipeline Running](10_github_actions_pipeline_running.png)

## 🔍 Pipeline Test Output  
![CI/CD Logs Success](16_ci_cd_pipeline_logs_success.png)

```
Test passed – app installed successfully!
```

## 💡 What I Learned

- Automating deployment pipelines using GitHub Actions  
- Writing workflow files in YAML  
- Testing APIs using curl inside CI/CD  
- Handling access tokens and GitHub authentication  

## 📣 Author  
**Oladapo Adenekan**  
GitHub: [https://github.com/oladapoade](https://github.com/oladapoade)

## 📌 Bonus Ideas  

- Add Docker + DockerHub integration  
- Add unit testing using pytest  
- Auto-deploy to AWS EC2, Heroku, or Render  

## ❗ Problems Faced & Solutions

### Problem 1: Virtual environment creation failed  
**Error:** `ensurepip is not available`  
✅ **Solution:**  
```bash
sudo apt install python3.12-venv
```

### Problem 2: App not showing up in browser  
✅ **Solution:** Verified Flask installation and visited `http://127.0.0.1:5000`

### Problem 3: GitHub push failed (403 error)  
✅ **Solution:** Used personal access token (PAT) to push:  
```bash
git push https://<username>:<token>@github.com/<username>/<repo>.git
```

### Problem 4: Simulate Test step missing in Actions  
✅ **Solution:** Added test step in `ci-cd.yml`:  
```yaml
- name: Simulate Test  
  run: |  
    python app.py &  
    sleep 3  
    curl http://127.0.0.1:5000
```

### Problem 5: Right-click not working in VS Code  
✅ **Solution:** Used terminal to create files:  
```bash
mkdir -p .github/workflows  
touch .github/workflows/ci-cd.yml
```

### Problem 6: GitHub Actions showed generic step names  
✅ **Solution:** Used `name:` field for clarity in workflow

### Problem 7: Terminal hiding files in VS Code  
✅ **Solution:** Collapsed terminal panel to access file view

### Problem 8: Forgot to commit README.md  
✅ **Solution:**  
```bash
git add README.md  
git commit -m "Added README"  
git push origin main
```

## ✅ Takeaway  
Each challenge helped improve my problem-solving, automation, and DevOps thinking. This is part of my journey into cloud engineering and CI/CD mastery.
