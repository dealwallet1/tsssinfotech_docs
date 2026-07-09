#  ANPR System — Full Technical Documentation
### Automatic Number Plate Recognition | YOLOv8 + EasyOCR + Google Colab

---

> **Version:** 1.0  
> **Platform:** Google Colab (T4 GPU)  
> **Language:** Python 3.x  
> **Status:** Production Ready

---

## Table of Contents

1. [What Is This System?](#1-what-is-this-system)
2. [How Does It Work?](#2-how-does-it-work)
3. [Models Used](#3-models-used)
4. [Live Video Display in Colab](#4-live-video-display-in-colab)
5. [Notebook Structure — Cell by Cell](#5-notebook-structure--cell-by-cell)
6. [Configuration Parameters](#6-configuration-parameters)
7. [Vehicle Classification](#7-vehicle-classification)
8. [What the Output Looks Like](#8-what-the-output-looks-like)
9. [How to Run — Step by Step](#9-how-to-run--step-by-step)
10. [Known Limitations](#10-known-limitations)
11. [Full Dependency List](#11-full-dependency-list)
12. [Glossary](#12-glossary)

---

## 1. What Is This System?

**ANPR** stands for **Automatic Number Plate Recognition.**

This system is a computer vision application that watches a video or image, automatically finds every vehicle in it, tells you what **type** of vehicle it is — Car, Truck, Bus, Motorcycle, or Bicycle — and then **reads the number plate text** from each vehicle. All of this happens in real time, frame by frame, as the video plays.

>  **In simple words:** Show it a traffic video. It finds the cars, names them, and reads their plates — automatically, as they drive past.

### Real-World Use Cases

- Traffic monitoring and law enforcement
- Toll booth automation
- Parking management systems
- Border control and vehicle logging
- Smart city and surveillance projects

Without this system, a human would need to manually watch hours of footage and note down plate numbers. This system does that work automatically.

---

## 2. How Does It Work?

Every frame of the video passes through **3 stages** in sequence:

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   INPUT FRAME (one frame from the video)                    │
│         │                                                   │
│         ▼                                                   │
│   ┌─────────────────┐                                       │
│   │   STAGE 1       │  YOLOv8n scans the full frame        │
│   │ Find Vehicles   │  → draws box around each vehicle     │
│   │                 │  → labels it: Car / Truck / Bus ...  │
│   └────────┬────────┘                                       │
│            │  (one crop per vehicle)                        │
│            ▼                                                │
│   ┌─────────────────┐                                       │
│   │   STAGE 2       │  Zooms into vehicle crop             │
│   │  Find Plate     │  → locates the number plate region   │
│   │                 │  → draws a yellow box around it      │
│   └────────┬────────┘                                       │
│            │  (plate crop image)                            │
│            ▼                                                │
│   ┌─────────────────┐                                       │
│   │   STAGE 3       │  EasyOCR reads the plate image      │
│   │   Read Text     │  → outputs: "MH 12 AB 3456"         │
│   │                 │  → overlaid on the video frame       │
│   └─────────────────┘                                       │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

| Stage | What Happens | Technology |
|-------|-------------|------------|
| Stage 1 | Full frame scanned, vehicles found and labelled | YOLOv8n — COCO pretrained |
| Stage 2 | Vehicle cropped, plate region located | YOLOv8n (plate model) or smart crop |
| Stage 3 | Plate image read, text extracted | EasyOCR |
| Output | Annotated frame streamed live / saved to video | OpenCV + JavaScript |

---

## 3. Models Used

### 3.1 YOLOv8n — Vehicle Detection Model

**YOLO** stands for **"You Only Look Once."** It is a family of very fast AI object detection models that can find and classify multiple objects in an image in a single pass — which is why it is fast enough for real-time video.

**YOLOv8n** is the **nano (n)** variant — the smallest and fastest version of the 8th generation of YOLO. It was created by **Ultralytics**.

| Property | Details |
|----------|---------|
| Full name | You Only Look Once — version 8, nano |
| Created by | Ultralytics |
| Model file size | ~6 MB (downloads automatically) |
| Speed | Real-time on GPU; usable on CPU |
| Trained on | COCO dataset — 80 object classes |
| What we use it for | Detecting and classifying vehicles |
| Vehicle classes used | Car (ID 2), Motorcycle (3), Bus (5), Truck (7), Bicycle (1) |
| Confidence threshold | 40% minimum — below this, detection is discarded |

>  **In plain language:** YOLOv8n is like a very fast pair of trained eyes. When you show it a frame from a traffic video, it instantly tells you: "There is a Car here, a Truck there, and a Motorcycle over there" — with bounding boxes drawn around each one.

---

### 3.2 YOLOv8n (Custom) — Plate Detection Model

After finding a vehicle, the system zooms into that vehicle crop to find the **number plate** specifically. A second YOLOv8n model, **fine-tuned on licence plate images**, is used for this.

This model is **optional.** If you don't have it, the system uses a **smart fallback**: it crops the bottom-centre 45% of the vehicle bounding box — because that is where number plates almost always appear on a vehicle.

| Property | Details |
|----------|---------|
| Base architecture | YOLOv8n (same as vehicle model) |
| Fine-tuned for | Detecting licence plate regions specifically |
| Input | Cropped vehicle image (not the full frame) |
| Output | Tight bounding box around the plate |
| Fallback | Heuristic bottom-centre crop if model not available |
| Confidence threshold | 35% minimum |

---

### 3.3 EasyOCR — Text Reading Model

**OCR** stands for **Optical Character Recognition** — the technology that reads text from images.

**EasyOCR** is a Python library built on deep learning (CRAFT for text detection + CRNN for text recognition) that reads text from images in over 80 languages.

| Property | Details |
|----------|---------|
| Library name | EasyOCR |
| Created by | JaidedAI |
| Technology | Deep learning — CRAFT + CRNN architecture |
| What it reads | Letters A–Z and digits 0–9 from plate images |
| Languages | English ("en") — add "hi" for Hindi plates |
| GPU support | Yes — ~5× faster on GPU than CPU |
| Pre-processing applied | Upscale to minimum 40px height + sharpening kernel filter |
| Character allowlist | Only `A-Z`, `0-9`, `-`, and space to reduce noise |

>  **In plain language:** EasyOCR is like a person who is very good at reading signs. Give it a cropped photo of a number plate, and it tells you exactly what letters and numbers are written on it.

---

### 3.4 OpenCV — Image & Video Processing

**OpenCV** (Open Source Computer Vision Library) is not an AI model — it is a toolkit for handling images and videos in Python. It handles all the visual input/output work: reading frames, drawing boxes and labels, and writing output files.

| Task | Function Used |
|------|--------------|
| Read video file frame by frame | `cv2.VideoCapture()` |
| Draw vehicle bounding boxes | `cv2.rectangle()` |
| Draw vehicle type labels | `cv2.putText()` |
| Draw plate text overlays | `cv2.putText()` |
| Write annotated output video | `cv2.VideoWriter()` |
| Compress frame for live display | `cv2.imencode('.jpg', ...)` |
| Sharpen plate crop before OCR | `cv2.filter2D()` with sharpening kernel |

---

## 4. Live Video Display in Colab

Google Colab runs on a **remote server** — there is no direct screen or media player pipeline. To make the detection look like a live video, the system uses a **JavaScript image-injection trick**:

**Step-by-step:**

1. An HTML `<img>` tag is injected into the Colab output cell using Python's `display(HTML(...))` function.
2. Each annotated frame is compressed to JPEG using OpenCV, then encoded to **Base64** — converting the image into a plain-text string.
3. A tiny JavaScript snippet runs and updates the `img.src` attribute with the new Base64 image. This replaces the displayed image instantly — creating the live video effect.
4. An **info bar** below the image also updates every frame, showing frame number, vehicle count, unique plates found, and FPS.
5. At the same time, every annotated frame is written to an output `.mp4` file on disk. When processing finishes, the full annotated video is **automatically downloaded** to your computer.

>  **Why not just play the video directly?** Colab has no media display pipeline from server to browser. The JavaScript image-swap trick is the standard workaround for streaming visuals from a Colab notebook in real time.

---

## 5. Notebook Structure — Cell by Cell

The notebook has **7 cells**. Run them in order from top to bottom.

| Cell | Name | What It Does |
|------|------|-------------|
| Cell 1 | **Install** | Installs: `ultralytics`, `easyocr`, `opencv-python-headless`, `gdown` |
| Cell 2 | **Imports & Config** | Imports all libraries, sets colour map for vehicle types, defines the `Det` dataclass, sets threshold values |
| Cell 3 | **Load Models** | Downloads + loads YOLOv8n (~6 MB auto-download), optionally loads plate model, loads EasyOCR (~100 MB first run) |
| Cell 4 | **Detection Functions** | Defines all functions: `clean_plate`, `run_ocr`, `process_frame`, `draw_frame`, `frame_to_b64`, `print_summary` |
| Cell 5 | ** MAIN CELL** | Upload image or video → auto-detects file type → runs full pipeline → streams live frames → downloads annotated output |
| Cell 6 | **Statistics** | Generates bar chart of vehicle types and donut chart of plate recognition rate |
| Cell 7 | **Tune Parameters** | Adjust confidence thresholds and skip-frame rate, then re-run Cell 5 |

---

## 6. Configuration Parameters

Three parameters control the system's speed and accuracy. They can be changed in **Cell 7** at any time.

| Parameter | Default | What It Controls |
|-----------|---------|-----------------|
| `CONF_VEHICLE` | `0.40` | Minimum confidence to accept a vehicle detection. Lower = catches more vehicles but risks false positives. |
| `CONF_PLATE` | `0.35` | Minimum confidence for the plate detection model. |
| `SKIP_FRAMES` | `2` | Process every (N+1)th frame. `0` = every frame (slowest, most accurate). `2` = every 3rd frame (faster, slightly less smooth). |

>  **Speed tip:** On a free Colab T4 GPU, `SKIP_FRAMES=2` gives roughly 3–5 FPS throughput. Set to `0` for maximum accuracy, or `3–4` for faster processing of long videos.

---

## 7. Vehicle Classification

YOLOv8n is trained on the **COCO dataset** (80 classes). The system filters this to only vehicle-related classes. Each vehicle type gets a distinct colour in the video overlay.

| Vehicle Type | COCO Class ID | Overlay Colour |
|-------------|--------------|---------------|
| Car | 2 | Cyan / Yellow |
| Motorcycle | 3 | Blue / Orange |
| Bus | 5 | Magenta / Purple |
| Truck | 7 | Green / Lime |
| Bicycle | 1 | Yellow / Cyan |
| Person | 0 | Light grey *(no plate OCR)* |
| Traffic Light | 9 | Dark grey *(no plate OCR)* |

> **Note:** Person and Traffic Light are detected and drawn but **plate OCR is not attempted** on them — they are tracked for scene context only.

---

## 8. What the Output Looks Like

### 8.1 Live Frame (during processing)

- **Coloured bounding box** around each detected vehicle
- **Vehicle label banner** (e.g. `Car 87%`) in a filled colour block at the top of the box
- **Yellow bounding box** around the detected plate region
- **Plate text banner** (e.g. `MH 12 AB 3456  91%`) in a black block at the bottom of the vehicle box
- **HUD bar** at the very top of the frame showing: frame number, FPS, and system name

### 8.2 Info Bar (below the live image)

Updates every processed frame and shows:

```
Frame 240/1800 (13%)  |  Vehicles: 4  |  Plates seen: 7  |  3.2 fps
```

### 8.3 Downloaded Output File

When the video finishes processing, a file named `anpr_<original_filename>.mp4` is automatically downloaded. This is a full MP4 with all detection overlays permanently baked in.

### 8.4 Summary Log (printed in cell output)

```
────────────────────────────────────────────────────────────
  Total vehicles  :  42
  Plates read     :  31  (74%)
  Unique plates   :  MH 12 AB 3456, KA 09 XY 7890, DL 4C AB 1234
────────────────────────────────────────────────────────────
```

---

## 9. How to Run — Step by Step

1. **Open** Google Colab at [colab.research.google.com](https://colab.research.google.com)
2. **Upload the notebook:** File → Upload notebook → select `ANPR_Live_Video_Detection.ipynb`
3. **Enable GPU:** Runtime → Change runtime type → select **T4 GPU** → Save
4. **Run Cell 1** — installs all packages *(takes ~30–60 seconds)*
5. **Run Cell 2** — imports and config *(instant)*
6. **Run Cell 3** — loads models *(YOLOv8 ~6 MB auto-download; EasyOCR ~100 MB on first run)*
7. **Run Cell 4** — defines all functions *(instant)*
8. **Run Cell 5** — click `Choose Files`, upload your `.mp4` or `.jpg`, and watch live detection begin
9. When done, the annotated video downloads automatically. Run **Cell 6** for statistics.

>  **Important:** Always run cells in order (1 → 2 → 3 → 4 → 5). If you restart the Colab runtime, start again from Cell 1. Loaded models do not persist between sessions.

---

## 10. Known Limitations

| Limitation | Explanation |
|-----------|------------|
| Night / low-light footage | YOLOv8 and EasyOCR perform worse in dark or underexposed conditions. Pre-brighten frames if needed. |
| Angled or small plates | Without the custom plate model, tilted or very small plates may be missed or misread. |
| Non-Latin scripts | EasyOCR defaults to English. Add language codes (e.g. `"hi"` for Hindi) in Cell 2 for regional plates. |
| Very fast-moving vehicles | High-speed vehicles may appear motion-blurred. Lower `SKIP_FRAMES` for better coverage. |
| Colab session time limit | Free Colab sessions disconnect after ~90 minutes of inactivity. Process long videos in segments. |
| Free GPU quota | Colab allocates GPU time fairly. You may occasionally get CPU-only runtime. Processing will be slower. |
| Occluded or damaged plates | Plates covered by dirt, physical damage, or other objects cannot be read by any OCR system. |

---

## 11. Full Dependency List

| Package | Version | Purpose |
|---------|---------|---------|
| `ultralytics` | `>=8.0.0` | YOLOv8 model loading, inference, and COCO class detection |
| `easyocr` | `>=1.7.0` | OCR engine — reads text from plate crop images |
| `opencv-python-headless` | `>=4.8` | Video I/O, frame drawing, image encoding |
| `numpy` | `>=1.24` | Array operations and image data manipulation |
| `torch` / `torchvision` | auto | Deep learning backend — installed automatically with ultralytics |
| `matplotlib` | built-in | Statistics charts in Cell 6 |
| `base64` | built-in | Encodes frames as text for JavaScript live display |
| `gdown` | optional | Downloads custom plate model from Google Drive |
| `yt-dlp` | optional | Downloads YouTube videos for processing |

**Install all at once:**

```bash
pip install ultralytics easyocr opencv-python-headless gdown -q
```

---

## 12. Glossary

| Term | Simple Explanation |
|------|--------------------|
| **ANPR** | Automatic Number Plate Recognition — the full system name |
| **YOLO** | "You Only Look Once" — an AI model family that detects objects in images very fast |
| **YOLOv8n** | 8th generation, nano (smallest/fastest) version of YOLO by Ultralytics |
| **COCO dataset** | A dataset of 330,000 images with 80 labelled object types, used to train YOLOv8 |
| **EasyOCR** | A Python library that reads text from images using deep learning |
| **OCR** | Optical Character Recognition — converting an image of text into actual text data |
| **Bounding box** | A rectangle drawn around a detected object in an image |
| **Confidence score** | A 0–100% number saying how certain the model is about a detection |
| **SKIP_FRAMES** | How many frames to skip between full inference passes — trades accuracy for speed |
| **Base64** | A way to convert binary image data into plain text so JavaScript can handle it |
| **Heuristic crop** | A rule-based guess: cut the bottom-centre area where plates usually appear |
| **Inference** | Running a trained AI model on new input data to get predictions |
| **FPS** | Frames Per Second — how many video frames are processed each second |
| **GPU** | Graphics Processing Unit — specialised hardware that makes AI inference much faster |
| **Fine-tuned** | Taking a general model (like YOLOv8n) and training it further on a specific task (like plates) |
| **Colab** | Google Colaboratory — free browser-based Python notebook environment with GPU access |

---

## Quick Reference Card

```
┌─────────────────────────────────────────────────┐
│              ANPR QUICK REFERENCE               │
├─────────────────────────────────────────────────┤
│  Stage 1 Model  │ YOLOv8n          (vehicles)  │
│  Stage 2 Model  │ YOLOv8n custom   (plates)    │
│  Stage 3 Engine │ EasyOCR          (text OCR)  │
│  Video I/O      │ OpenCV                        │
├─────────────────────────────────────────────────┤
│  CONF_VEHICLE   │ 0.40  (lower = more detects) │
│  CONF_PLATE     │ 0.35                          │
│  SKIP_FRAMES    │ 2     (0 = every frame)      │
├─────────────────────────────────────────────────┤
│  Supported in   │ .jpg .png .mp4 .avi .mov     │
│  Supported out  │ .jpg image  /  .mp4 video    │
├─────────────────────────────────────────────────┤
│  Run order      │ Cell 1 → 2 → 3 → 4 → 5      │
│  GPU needed     │ T4 GPU (Colab free tier)      │
└─────────────────────────────────────────────────┘
```

---

*ANPR System — YOLOv8 + EasyOCR — Google Colab — v1.0*