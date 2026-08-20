# Urdu OCR — Extracting Text from Urdu Images with a Fine-Tuned TrOCR Model

**By Warood** · Built during the Code Saviours ML/AI Internship — Batch SI-26

---

##  The Problem

Urdu is spoken by over 230 million people worldwide, yet it remains one of the most under-served languages in Optical Character Recognition (OCR) technology. Unlike English or other Latin-script languages, Urdu is written in a cursive, right-to-left Nastaliq script where character shapes change depending on their position in a word — making it significantly harder for standard OCR systems to read accurately.

This gap has real consequences: newspapers, historical books, handwritten letters, signboards, and government documents in Urdu remain largely inaccessible to digital search, translation, and archiving tools. A student researching old Urdu newspaper archives, a company trying to digitize Urdu paperwork, or a translation app trying to support Urdu speakers all run into the same wall — there simply isn't enough reliable, open-source Urdu OCR tooling available.

This project is an attempt to explore that gap directly: **can a modern transformer-based OCR model be adapted to read Urdu text, and what does it actually take to get there?**

---

##  How It Works

At the core of this project is **TrOCR** (Transformer-based Optical Character Recognition), a model developed by Microsoft that combines two components:

- A **vision encoder** that "looks" at an image and understands its visual structure
- A **text decoder** that converts what the encoder sees into readable text

TrOCR is originally trained on printed **English** text. To adapt it for Urdu, I used a technique called **fine-tuning** — taking the pretrained model and continuing its training on a new, smaller dataset (in this case, labeled Urdu text images) so it can learn to recognize Urdu characters and patterns instead.

The project was broken into five stages:
1. **Dataset collection** — gathering and labeling real Urdu text images
2. **Preprocessing & baseline testing** — understanding how existing OCR tools (like Tesseract) handle Urdu, and why they fall short
3. **Dataset expansion & pipeline building** — growing the dataset and wrapping it in a PyTorch-compatible data pipeline
4. **Model training & evaluation** — fine-tuning TrOCR and measuring its real-world accuracy
5. **Deployment** — packaging the trained model into a live, publicly usable web app

---

##  Live Demo

Try the model yourself — upload any image containing Urdu text and see what it extracts:

**[ Launch the Urdu OCR App](https://huggingface.co/spaces/waroodzkhan/urdu-ocr-codesaviours-si26-warood)**

---

##  How to Run It Locally

1. **Clone this repository**
   ```bash
   git clone https://github.com/waroodzahrakhan/urdu-ocr-codesaviours-si26-warood.git
   cd urdu-ocr-codesaviours-si26-warood
   ```

2. **Install dependencies**
   ```bash
   pip install transformers torch pillow gradio
   ```

3. **Download the fine-tuned model**
   The trained model is hosted on HuggingFace at [`waroodzkhan/urdu-ocr-si26-model`](https://huggingface.co/waroodzkhan/urdu-ocr-si26-model). It will be downloaded automatically the first time you run the app.

4. **Run the app**
   ```bash
   python app.py
   ```

5. Open the local URL printed in your terminal, upload an Urdu image, and see the extracted text.

---

##  Dataset Details

The dataset was built entirely from scratch over the course of this internship, growing from 101 to 201 labeled images:

| Detail | Description |
|---|---|
| **Total images** | 201 (191 used after cleaning) |
| **Sources** | UHAT dataset, real newspaper screenshots (Jang & Dawn Urdu), synthetically generated text images |
| **Categories** | Newspapers, books, signboards, synthetic text, other |
| **Variety captured** | Multiple fonts, backgrounds, and text sizes across printed and digitally generated sources |
| **Labeling** | Every image manually verified and corrected for accurate Urdu text transcription |
| **Split** | 80% training (152 images) / 20% testing (39 images) |

---

##  Results

**Model accuracy: 0.0% (0/39 correct on the test set)**
**Training loss went from 17.8888 → 0.8349** across 3 epochs, showing the model was actively learning patterns from the training data — even though that learning didn't translate into correct predictions on unseen Urdu text.

### Why the accuracy was low

The core issue isn't a bug — it's a fundamental mismatch. `microsoft/trocr-base-printed`, the base model used for fine-tuning, was pretrained exclusively on **English** text. Its tokenizer and vocabulary were never built to represent Urdu Unicode characters, so even after fine-tuning, the model's outputs were largely placeholder/unknown-character symbols rather than valid Urdu script.

Fine-tuning nudged the model's internal weights toward the *shapes* and *patterns* in the Urdu training images (which is why the training loss dropped meaningfully), but it couldn't overcome the vocabulary-level limitation baked into the base model — and with only ~150 training images, there also wasn't nearly enough data to teach a from-scratch understanding of an entirely new script.

### What I would do differently with more time

- Start from a **multilingual or Urdu-specific OCR base model** instead of an English-only one, so the vocabulary already supports Urdu Unicode
- Scale the dataset from hundreds to **thousands of labeled images** for genuine generalization
- Experiment with **character-level or byte-level tokenization** better suited to non-Latin scripts
- Apply stronger data augmentation (rotation, noise, varied fonts) to build robustness

---




