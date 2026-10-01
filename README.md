# 🎥 AI Video Watermark Remover Pipeline

An end-to-end, automated video processing pipeline that removes watermarks, logos, and text overlays from videos using state-of-the-art AI video inpainting. 

This project provides a wrapper workflow designed to be run in Google Colab (or locally with a dedicated GPU). It handles the complete lifecycle of the video processing task: extracting frames and audio, generating precision coordinate-based masks, running the intensive AI inpainting process, and reassembling the final clean video.

## ✨ Features
* **Automated Frame & Audio Extraction:** Utilizes `FFmpeg` to losslessly separate the video into individual frames and isolate the audio track.
* **Precision Mask Generation:** Uses `OpenCV` to draw exact bounding-box masks over the targeted watermark coordinates.
* **Memory-Optimized AI Processing:** Configured to run heavy optical-flow inpainting models on standard free cloud GPUs (like Google Colab's T4) without crashing due to out-of-memory (OOM) errors.
* **Lossless Reassembly:** Automatically stitches the repaired frames back together and merges the original audio track for a seamless final product.
* **Visualizer Tool:** Includes an integrated Matplotlib grid visualizer to help pinpoint exact pixel coordinates for the mask.

## 🛠️ Tech Stack
* **Python 3.x**
* **OpenCV** (Mask generation and computer vision)
* **FFmpeg** (Video/audio demuxing and muxing)
* **PyTorch** (AI model execution)
* **ProPainter** (Core video inpainting engine)

## 🚀 Try It Yourself
You can run this entire pipeline directly in your browser without installing anything locally.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](INSERT_YOUR_COLAB_LINK_HERE)

### How to use:
1. Open the Colab Notebook using the link above.
2. Upload your target `.mp4` video.
3. Run the visualizer cell to find the exact `X`, `Y`, `WIDTH`, and `HEIGHT` coordinates of the watermark.
4. Execute the pipeline to extract, mask, inpaint, and rebuild the video.

## 🧠 How It Works
Unlike standard image inpainting, video inpainting requires **temporal consistency**. If an AI just guesses the background frame-by-frame, the video will flicker aggressively. This pipeline utilizes Dual-Domain Spatial-Temporal Transformers to analyze the motion (optical flow) of the frames *before* and *after* the current frame, allowing it to intelligently borrow background pixels from other parts of the video to fill in the masked hole smoothly.

## ⚖️️ Credits & Acknowledgements
* **Pipeline & Automation:** Vikas Yadav (B.Tech, Artificial Intelligence & Machine Learning)
* **Core AI Engine:** This project leverages the [ProPainter](https://github.com/sczhou/ProPainter) model by sczhou for the underlying video inpainting inference. All credit for the neural network architecture and pre-trained weights goes to the original researchers. Please refer to their repository for the model's specific open-source license.
