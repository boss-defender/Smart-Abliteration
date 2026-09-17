# Abliteration

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/boss-defender/Smart-Abliteration/blob/main/Decensor_Ai_Model_heretic.ipynb)

Created using Colab and Heretic tool for AI model abliterating.  

# 🗡️ Heretic Colab Decensor: Uncensor LLMs easily 🔥

Transform restricted, refusal-heavy AI models into completely open, unfiltered powerhouses right inside Google Colab — no expensive local hardware required! 🚀

This repository provides a simple, zero-setup **Google Colab Interface** powered by [**Heretic**](https://github.com/p-e-w/heretic). Just paste your favorite Hugging Face model name, hit play, and walk away with your freshly uncensored model zipped up and ready to download!

---

## 🧠 What Is This & How Does It Work?

When AI models refuse to answer questions, it's because safety alignment places specific "refusal directions" inside their mathematical layers. 

Older tools used brute force to chop these out, which often caused severe AI brain damage 🥴. **Heretic** acts like a precision surgeon:

* 🎯 **Refusal Direction Tracking:** It scans the model's internal residual streams to pinpoint exactly where the refusal logic lives.
* ⚖️ **Smart Optimization:** It automatically calculates optimal ablation weights using Optuna, keeping your model sharp while removing the guardrails (minimizing KL-divergence).
* ⚡ **Low-VRAM Magic:** Runs in `BNB_4BIT` mode so you can process 7B to 12B parameter models on a **Free Google Colab T4 GPU** without crashing memory!

---

## 🚀 How to Use (Step-by-Step)

### 1️⃣ Open in Colab

Click here to **[Open in Colab](https://colab.research.google.com/github/boss-defender/Abliteration/blob/main/Decensor_Ai_Model_heretic.ipynb)** or upload the `Decensor_Ai_Model_heretic.ipynb` notebook to Google Colab.

### 2️⃣ Turn on the GPU
Go to **Runtime** ➡️ **Change runtime type** ➡️ Select **T4 GPU** ➡️ Click **Save**.

### ⚡PRO TIP / RUN-ALL NOTE:
You can simply click **Runtime ➡️ Run all** (`Ctrl + F9` / `Cmd + F9`) to run the whole pipeline automatically! Just make sure you set your correct **Hugging Face Model Path** (`MODEL_NAME e.g., Qwen/Qwen2.5-7B-Instruct`), **Quantization** (`BNB_4BIT`), and **Access Token** (only if using a gated model) in Cell 1 & **Correct File Path** in Cell 2 & 3 **before** hitting Run All! 🎯.

**Note: A Google Drive permission pop-up will appear when Cell 1 runs—simply click "Connect to Google Drive -> select google account -> select all permission" to enable automatic checkpoint saving! 📁**

### 3️⃣ Step 1: Configure , Install Engine & Decensor

Fill in the form fields on Cell 1 and click **Play (▶️)**.
This checks your GPU availability and installs `heretic-llm` and its required tools and starts decensoring. 

* **`MODEL_NAME`**: Paste any Hugging Face model path (e.g., `Qwen/Qwen2.5-7B-Instruct`).
* **`QUANTIZATION`**: Keep as `BNB_4BIT` for free Colab VRAM, or set to `NONE` if you have Colab Pro.
* **`HUGGINGFACE_TOKEN`**: *(Optional)* Paste your token if using gated models like `meta-llama/Llama-3.1-8B-Instruct`.
* **`GOOGLE DRIVE AUTHORIZATION`**: When prompted by the pop-up window, click "Connect to Google Drive -> select google account -> select all permission". This allows the script to create a tiny checkpoint folder (~10-50 MB) to save your trial progress in real-time! 💾

### 4️⃣ Step 2: Zip Output Files
Click **Play (▶️)** on Cell 2. It smart-scans your workspace, finds your newly decensored model weights, and packs them into a `.zip` archive. I don't prefer to zip folder. You may need to be extra careful about path while zipping. 

### 5️⃣ Step 3: Download Model
Click **Play (▶️)** on Cell 3. This triggers an automatic browser download straight to your computer! You may need to be extra careful while downloading. It will be best to manually download. But for large file, just copy path of that large file and paste in zip_file -> path. then click start. It will download large file if you face errors/abort message while manually downloading .📦⬇️ 

### ⏳ And yes, it will take a long time to finish. Don't worry, keep that tab open. And take a movie break.
---

**💫 Heretic Export Cheat Sheet**

* When trials finish, enter these inputs in sequence:

* Select Best Trial: 1 (Lowest refusal score)

* Export Action: 1 (Save to local folder)

* Output Path: /content/uncensoredai

* Merge Method: 1 (Merge LoRA & export full model)

* ⏳ Wait for Writing model shards: 100% to complete!

* Back to Menu: 5

* Exit Program: 14 / 10 (or the number for Exit)


---

# **🧠 Caution !**


💡 **Always download tokenizer_config.json from hugging face base model.**

🚩 **Because Heretic will give you Broken tokenizer_config.json ! 🚨** 

💡 **Download llama.cpp and Install it. After installing llama.cpp properly use this command below to generate GGUF file to run AI model in LMstudio or Ollama**

---

**🪄 Single Line Command Prompt**
---

🎯 **python convert_hf_to_gguf.py "/path/to/dir/[Folder Name Where All Files Saved]" --outfile "/path/to/dir/[AI Model Name].gguf" --outtype auto**

or,

🎯 **./venv/bin/python convert_hf_to_gguf.py "/path/to/dir/[Folder Name Where All Files Saved]" --outfile "/path/to/dir/[AI Model Name].gguf" --outtype auto**

---

**👇 If you want Q4_K_M or anyother format**
---

🎯 **python convert_hf_to_gguf.py "/path/to/dir/[Folder Name Where All Files Saved]" --outfile "/path/to/dir/[Temp Name].gguf" --outtype f16 && ./llama-quantize "/path/to/dir/[Temp Name].gguf" "/path/to/dir/[Final Name].gguf" Q4_K_M && rm "/path/to/dir/[Temp Name].gguf"**

or,

🎯 **./venv/bin/python convert_hf_to_gguf.py "/path/to/dir/[Folder Name Where All Files Saved]" --outfile "/path/to/dir/[Temp Name].gguf" --outtype f16 && ./build/bin/llama-quantize "/path/to/dir/[Temp Name].gguf" "/path/to/dir/[Final Name].gguf" Q4_K_M && rm "/path/to/dir/[Temp Name].gguf"**

---

## 🛡️ Crash-Proof Auto-Resume (Disconnect Without Fear!)

💡 **ACCIDENTAL MISTAKE OR GOING TO BED? NO PROBLEM!** 🔌😴⚡

Whether life happens by accident (sudden power outage, accidental tab close, browser crash) OR you intentionally shut down your PC to catch some sleep 🛌—**your progress is 100% safe!**

You never need to leave your computer running all night. Whenever you're ready to continue:

1. Re-open Google Colab anytime later.
2. Paste the **exact same model name** you were working on.
3. Hit **Play (▶️)**!
4. Use same google drive account where heretic_checkpoints saved.
5. Wait till it finishes.

The script automatically mounts your Google Drive, detects your saved checkpoint, skips all finished trials, and instantly picks up right where you left off! 🔄💾

**You need to select either you want to Continue the previous run or start from scratch. Type 1 and hit enter**

## 🔄 Resuming Progress After GPU Timeout (Free Tier)

Ran out of free Colab GPU hours mid-run? Don't panic! All trial progress is auto-saved directly to Google Drive. Here is how to keep cooking without losing a single step:


### ⏳ Option A: Resume on the Same Account (After Quota Reset)
1. Open the notebook after your GPU access resets (usually 24 hours).
2. Connect to a GPU runtime and hit **Run** on Cell 1.
3. The engine automatically detects your `heretic_checkpoints` folder on Google Drive and picks up right where it got cut off! 🚀

### ⚡ Option B: Switch to a 2nd Google Account (Immediate Resume)
Don't want to wait 24 hours? Jump to another Gmail account and keep going immediately:

1. **Share the Checkpoints Folder** 📤
   * Open Google Drive on **Account #1**.
   * Right-click the `heretic_checkpoints` folder ➔ **Share** ➔ Add **Account #2's Gmail** (set permission to **Editor**).

2. **Add Folder or Create Shortcut in Account #2's Drive** 🔗
   * Open Google Drive on **Account #2** and go to **Shared with me** on the left menu.
   * Right-click the `heretic_checkpoints` folder and select **Add shortcut** (or **Organize** ➔ **Add shortcut**). Alternatively, you can drag and move the folder directly into **My Drive**.
   * Pick **My Drive** as the location so Colab maps it cleanly to `/content/drive/MyDrive/heretic_checkpoints`.

3. **Run the Notebook on Account #2** 🚀
   * Open the Colab notebook signed in as **Account #2**.
   * Set runtime to **GPU** and run **Cell 1**.
   * `heretic` will read the shared checkpoint folder and seamlessly continue from the last saved trial! 🎉

**You need to select either you want to Continue the previous run or start from scratch. Type 1 and hit enter**

---

## ✨ Key Features

* 🎛️ **Zero-Code Form GUI:** No messing around with raw terminal commands.
* 🛡️ **Anti-OOM Safeguards:** Optimized 4-bit quantization modes prevent out-of-memory errors on free GPUs.
* 📂 **No-Drama Auto Zipping:** Automatically locates output files no matter where Heretic saves them.
* ⚡ **1-Click Automation:** Full support for running the entire notebook sequentially in one shot!

---

## 📜 Credits & Acknowledgments

* Engine powered by [p-e-w/heretic](https://github.com/p-e-w/heretic).
* Workflow inspired by Plinius's OBLITERATUS notebook series.
