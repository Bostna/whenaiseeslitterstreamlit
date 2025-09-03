# WhenAISeesLitterStreamlit  

**Real-time litter detection with Streamlit & YOLO**  
A simple and interactive web app to detect litter using a local YOLO model via Streamlit.

---

##  Demo

> *(Include a screenshot or animated GIF here showing the app in action: webcam feed detecting litter or an uploaded image with bounding boxes.)*

---

## Features

- Leverages [Streamlit](https://streamlit.io) for a responsive web UI  
- Runs YOLO object detection with a local model (`best.pt`)  
- Upload images or use a live webcam stream for inference  
- Easily configurable environment and model options  

---

## Contents

| File | Description |
|------|-------------|
| `streamlit_app.py` | Main application logic and Streamlit UI |
| `requirements.txt` | Python dependencies to install |
| `best.pt` | YOLO model weights (rename your trained weights to this file name) |

---

## Setup

```bash
# Create and activate a virtual environment
python -m venv .venv
source .venv/bin/activate           # On Windows: .venv\Scripts\activate

# Install dependencies
pip install --upgrade pip
pip install -r requirements.txt
```bash
Usage
streamlit run streamlit_app.py
The app will launch at http://localhost:8501.
Upload an image or toggle the webcam mode, then click "Run detection" to see results in real time!

Configuration Notes
Use custom weights
Rename your model or set an environment variable:
export LOCAL_MODEL=my_model.pt
PyTorch on Apple Silicon
If torch installs slowly, try:
pip install 'torch==2.4.*' --extra-index-url https://download.pytorch.org/whl/cpu
