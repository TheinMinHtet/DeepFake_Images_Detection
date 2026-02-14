# Deepfake_Images_Detection
Deepfake_Images_Detection is a Deepfake Detection website where you can check if a video or photo is real or if it has been tampered with. It’s built for anyone who wants to make sure what they are seeing online is the truth.

## 🐍 Option 1: Run Locally with Python

1. Clone the repository:

```bash
git clone https://github.com/TheinMinHtet/Deepfake_Images_Detection
cd Deepfake_Images_Detection
```

2 Create a virtual environment:
```bash
python -m venv venv
# Windows
venv\Scripts\activate
# Mac/Linux
source venv/bin/activate
```

3.Install dependencies:
```bash
pip install -r requirements.txt
```

4.Run the FastAPI server:
```bash
python -m app/main.py
```

5.Open the API docs in your browser:
```bash
http://localhost:8000/docs
```
------------------------------------
## 🐳 Option 2: Run with Docker

1.Clone the repository:
```bash
git clone https://github.com/TheinMinHtet/Deepfake_Images_Detection
cd Deepfake_Images_Detection
```

2.Build the Docker image:
```bash
docker build -t Deepfake_Images_Detection .
```

3.Run the Docker container:
```bash
docker run -p 8000:8000 -v "C:/Users/Asus/Desktop/weights:/app/weights" Deepfake_Images_Detection
```
4.Access API docs:
```bash
http://localhost:8000/docs
```
