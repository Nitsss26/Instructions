ANPR System - Quick Start GuideThis guide allows anyone to run the ANPR system with a single copy-paste command.📋 PrerequisitesInstall Docker Desktop: Download here and install it.Open the App: Make sure Docker Desktop is running in the background.🚀 How to StartChoose your operating system, copy the code block, paste it into your terminal, and hit Enter.🍎 For Mac & 🐧 Linux Users (Terminal)Copy and paste this entire block at once:echo "--- Setup ANPR System ---"; \
mkdir -p raw_detections detected_plates uploads; \
read -p "Enter your GEMINI_API_KEY: " API_KEY; \
if [ -z "$API_KEY" ]; then echo "❌ Key is empty!"; else \
docker run -d --name anpr-frontend -p 3000:3000 -e NEXT_PUBLIC_BACKEND_URL=http://localhost:9000 nitti001/anpr-frontend:latest; \
docker run -d --name anpr-backend -p 9000:5000 -e GEMINI_API_KEY="$API_KEY" -v "$PWD/raw_detections:/app/raw_detections" -v "$PWD/detected_plates:/app/detected_plates" -v "$PWD/uploads:/app/uploads" nitti001/anpr-backend:latest; \
echo "✅ System Running!"; \
echo "Frontend: http://localhost:3000"; \
docker logs -f anpr-backend; \
fi
🪟 For Windows Users (PowerShell)Open PowerShell, then copy and paste this entire block:$API_KEY = Read-Host "Enter your GEMINI_API_KEY"
if ([string]::IsNullOrWhiteSpace($API_KEY)) { Write-Host "❌ Key cannot be empty" -ForegroundColor Red } else {
    New-Item -ItemType Directory -Force -Path raw_detections, detected_plates, uploads | Out-Null
    docker run -d --name anpr-frontend -p 3000:3000 -e NEXT_PUBLIC_BACKEND_URL=http://localhost:9000 nitti001/anpr-frontend:latest
    docker run -d --name anpr-backend -p 9000:5000 -e GEMINI_API_KEY=$API_KEY -v ${PWD}/raw_detections:/app/raw_detections -v ${PWD}/detected_plates:/app/detected_plates -v ${PWD}/uploads:/app/uploads nitti001/anpr-backend:latest
    Write-Host "✅ System Running!" -ForegroundColor Green
    Write-Host "Frontend: http://localhost:3000"
    docker logs -f anpr-backend
}
🛑 How to StopWhen you are done, run this command to stop and clear everything.🍎 Mac / 🐧 Linuxdocker stop anpr-backend anpr-frontend && docker rm anpr-backend anpr-frontend
🪟 Windows (PowerShell)docker stop anpr-backend anpr-frontend; docker rm anpr-backend anpr-frontend
