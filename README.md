# 🚗 ANPR System (AI License Plate Detection)

This project uses Artificial Intelligence to detect license plates from video feeds. This guide is designed for everyone---you do not need to be a technical expert to run this!

---

## 🛠️ Step 1: Prerequisites (Do this first)

Before starting the app, you need to set up two things.

### 1. Install Docker Desktop

Docker is the tool that runs the application on your computer.

* **Download:** [Click here to Download Docker Desktop](https://www.docker.com/products/docker-desktop/)

* **Tutorial Video:** [How to Install Docker](https://www.youtube.com/watch?v=JBEUKrjbWqg)

* **⚠️ Important:** After installing, open the "Docker Desktop" app and make sure it is running in the background.

### 2. Get a FREE Gemini API Key

This key allows the AI (Google Gemini) to read the license plates.

* **Get Key:** [Click here to get your API Key](https://aistudio.google.com/app/apikey)

* **Tutorial Video:** [How to get your API Key](https://www.youtube.com/watch?v=czN-laeLxr8)

* *Copy your key and keep it ready!*

---

## 🚀 Step 2: Start the Application

Select your operating system below. Copy the code block, paste it into your terminal, and press **Enter**.

### 🪟 For Windows Users

1\. Search for **PowerShell** in your Start Menu and open it.

2\. Copy the entire block below and paste it → press **Enter**

3\. Paste your **GEMINI_API_KEY** when prompted → press **Enter** (press Enter again if needed)

```bash:disable-run

$API_KEY = Read-Host "Paste your GEMINI_API_KEY here"

if ([string]::IsNullOrWhiteSpace($API_KEY)) { Write-Host "❌ Key cannot be empty" -ForegroundColor Red } else {

    New-Item -ItemType Directory -Force -Path raw_detections, detected_plates, uploads | Out-Null

    docker run -d --name anpr-frontend -p 3000:3000 -e NEXT_PUBLIC_BACKEND_URL=http://localhost:9000 nitti001/anpr-frontend:latest

    docker run -d --name anpr-backend -p 9000:5000 -e GEMINI_API_KEY=$API_KEY -v ${PWD}/raw_detections:/app/raw_detections -v ${PWD}/detected_plates:/app/detected_plates -v ${PWD}/uploads:/app/uploads nitti001/anpr-backend:latest

    Write-Host "✅ System Started Successfully!" -ForegroundColor Green

    Write-Host "🌍 Open this link in your browser: http://localhost:3000"

    docker logs -f anpr-backend

}
```

### 🍎 For Mac & 🐧 Linux Users

1\. Open your **Terminal**.

2\. Copy the entire block below and paste it → press **Enter**

3\. Paste your **GEMINI_API_KEY** when prompted → press **Enter** (press Enter again if needed)

```bash:disable-run

echo "--- Setup ANPR System ---";

mkdir -p raw_detections detected_plates uploads;

read -p "Paste your GEMINI_API_KEY here: " API_KEY;

if [ -z "$API_KEY" ]; then echo "❌ Key cannot be empty!"; else

docker run -d --name anpr-frontend -p 3000:3000 -e NEXT_PUBLIC_BACKEND_URL=http://localhost:9000 nitti001/anpr-frontend:latest;

docker run -d --name anpr-backend -p 9000:5000 -e GEMINI_API_KEY="$API_KEY" -v "$PWD/raw_detections:/app/raw_detections" -v "$PWD/detected_plates:/app/detected_plates" -v "$PWD/uploads:/app/uploads" nitti001/anpr-backend:latest;

echo "✅ System Started Successfully!";

echo "🌍 Open this link in your browser: http://localhost:3000";

docker logs -f anpr-backend;

fi
```
---

## 🌐 Step 3: Use the App

Once the command above is running:

* Open your web browser (Chrome, Safari, etc.).

* Go to: http://localhost:3000

* (Note: The terminal window will show you logs of what the AI is doing. You can minimize it, but don't close it.)

---

## 🛑 Step 4: How to Stop

When you are done using the application, run this command to stop and clean up.

### For Windows (PowerShell):

1\. In the Terminal where logs are running → press **Ctrl + C** (this stops the live logs)

2\. Then run this single command:

```bash:disable-run
docker stop anpr-backend anpr-frontend; docker rm anpr-backend anpr-frontend
```

### For Mac / Linux:

1\. In the Terminal where logs are running → press **Ctrl + C** (this stops the live logs)

2\. Then run this single command:

```bash:disable-run
docker stop anpr-backend anpr-frontend && docker rm anpr-backend anpr-frontend
```

---
