# 🚗 ANPR System (AI License Plate Detection)

This software uses Artificial Intelligence to detect license plates from video feeds. This guide is designed for everyone.

---

## 🛠️ Step 1: Prerequisites (Do this first)

Before starting the app, you need to set up two things.

### 1. Install Docker Desktop

Docker is the tool that runs the application on your computer.

* **Download:** [Click here to Download Docker Desktop](https://www.docker.com/products/docker-desktop/)

* **Tutorial Video:** [How to Install Docker](https://www.youtube.com/watch?v=JBEUKrjbWqg)

* **⚠️ Important:** After installing, open the "Docker Desktop" app and keep it running in the background at all times while using the app (when done, press Ctrl+C in terminal first, then quit Docker Desktop via the three dots ⋯ in the bottom-left corner → Quit Docker Desktop).

### 2. Get a FREE Gemini API Key

This key allows the AI (Google Gemini) to read the license plates.

* **Get Key:** [Click here to get your API Key](https://aistudio.google.com/app/apikey)

* **Tutorial Video:** [How to get your API Key](https://www.youtube.com/watch?v=czN-laeLxr8)

* *Copy your api key and keep it ready!*

---

## 🚀 Step 2: Start the Application

Select your operating system below. Copy the code block, paste it into your terminal, and press **Enter**.

### 🪟 For Windows Users

1\. Search for **PowerShell** in your Start Menu and open it.

2\. Create a folder named ANPR on your Desktop then copy the entire block below and paste it into your terminal → press **Enter**

```bash:disable-run
cd Desktop/ANPR
```

3\. Copy the entire block below and paste it into your terminal → press **Enter**

```bash:disable-run
docker run -d --name anpr-frontend -p 3000:3000 -e NEXT_PUBLIC_BACKEND_URL=http://localhost:9000 nitti001/anpr-frontend:v2.1
```

4\. Copy the entire block below, replace "AIzaSyCOCBpcPbLUTVaaqLnS_XXXXXXXXX" with your actual API key, then paste it into your terminal → press **Enter**
```bash:disable-run
docker run -d --name anpr-backend -p 9000:5000 -e GEMINI_API_KEY=AIzaSyCOCBpcPbLUTVaaqLnS_XXXXXXXXX -v "$PWD/raw_detections:/app/raw_detections" -v "$PWD/detected_plates:/app/detected_plates" -v "$PWD/uploads:/app/uploads" -v "$PWD/rejected_plates:/app/rejected_plates" nitti001/anpr-backend:v2.1
```

5\. Copy the entire block below and paste it → press **Enter**

```bash:disable-run
docker logs -f anpr-backend
```

### 🍎 For Mac & 🐧 Linux Users

1\. Open your **Terminal**.

2\. Create a folder named ANPR on your Desktop then copy the entire block below and paste it into your terminal → press **Enter**

```bash:disable-run
cd Desktop/ANPR
```

3\. Copy the entire block below and paste it into your terminal → press **Enter**

```bash:disable-run
mkdir -p raw_detections detected_plates uploads rejected_plates
```

4\. Copy the entire block below and paste it into your terminal → press **Enter**

```bash:disable-run
docker run -d --name anpr-frontend -p 3000:3000 -e NEXT_PUBLIC_BACKEND_URL=http://localhost:9000 nitti001/anpr-frontend:v2.1
```

5\. Copy the entire block below, replace "AIzaSyCOCBpcPbLUTVaaqLnS_XXXXXXXXX" with your actual API key, then paste it into your terminal → press **Enter**

```bash:disable-run
docker run -d --name anpr-backend -p 9000:5000 -e GEMINI_API_KEY=AIzaSyCOCBpcPbLUTVaaqLnS_XXXXXXXXX -v "$PWD/raw_detections:/app/raw_detections" -v "$PWD/detected_plates:/app/detected_plates" -v "$PWD/uploads:/app/uploads" -v "$PWD/rejected_plates:/app/rejected_plates" nitti001/anpr-backend:v2.1
```

6\. Copy the entire block below and paste it → press **Enter**

```bash:disable-run
docker logs -f anpr-backend
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

### 🪟 For Windows (PowerShell):

1\. In the Terminal where logs are running → press **Ctrl + C** (this stops the live logs)

2\. Then run this single command:

```bash:disable-run
docker stop anpr-backend anpr-frontend; docker rm anpr-backend anpr-frontend
```
3\. Quit Docker Desktop via the three dots ⋯ in the bottom-left corner → Quit Docker Desktop

### 💻 For Mac / Linux:

1\. In the Terminal where logs are running → press **Ctrl + C** (this stops the live logs)

2\. Then run this single command:

```bash:disable-run
docker stop anpr-backend anpr-frontend && docker rm anpr-backend anpr-frontend
```
3\. Quit Docker Desktop via the three dots ⋯ in the bottom-left corner → Quit Docker Desktop

---


