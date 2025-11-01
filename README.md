# AutoCut: AI-Powered Event Video
### EventVision Hackathon Submission by Team X-Pointers

**Team Members:** Tanish Kumar, Sambhav Jain, Shobhit Chola

---

## Overview

"AutoCut" is a fully automated Python pipeline that transforms long, raw event footage into a short, "cinematic" highlight video. It addresses the tedious manual process of sifting through hours of clips by using AI to analyze, score, and assemble the best moments.

## 📺 Final Demo

Our pipeline processed 13 raw clips (12.5 minutes) and automatically generated this 7.74-minute final video.

**[Click here to watch the final video (Link to your Unlisted YouTube or Google Drive video)]**

---

## 🛠️ Technical Approach

Our system is a 4-stage modular pipeline:

1.  **Analysis:** Uses `PySceneDetect` to split videos into 79 individual shots. It then uses `OpenCV` to analyze each shot for:
    * **Blur/Sharpness** (Laplacian Variance)
    * **Face Presence** (Haar Cascades)
    * **Motion/Shakiness** (Optical Flow)
    * The output is a `shot_analysis_results.csv` (sample included in this repo).

2.  **Scoring (The "AI Brain"):** We apply a weighted "Interest Score" to each shot based on our normalized features. This formula acts as our "AI Editor," prioritizing clear, stable, face-focused shots.

3.  **Selection:** The pipeline automatically rejects all "bad" shots (too blurry, too short, or too shaky) and selects the top-scoring shots to fit a 5-10 minute target.

4.  **Assembly:** Uses `MoviePy` to stitch the selected clips, add 0.5s cross-fade transitions for fluidity, and replace the original audio with a new background music track.

---

## 🚀 How to Run

1.  **Environment:** This project is built to run in a Kaggle Notebook with a T4 GPU.
2.  **Dependencies:** `scenedetect`, `moviepy`, `opencv-python` (all installed via `pip`).
3.  **Run:** Open `autocut_pipeline.ipynb` and run all cells from top to bottom.
4.  **Input:** The notebook is designed to read video clips from `/kaggle/input/` (like our `short-clips` dataset) and music from `/kaggle/input/` (like our `musicc` dataset).
