<div align="center">

# Audio8 ASR Infinite: Speech Recognition Tool

![Release Date](https://img.shields.io/github/created-at/D4rk-Pho3nix/OpenSauce?style=flat-square&label=released&color=green)
![Last Commit](https://img.shields.io/github/last-commit/D4rk-Pho3nix/OpenSauce?style=flat-square&label=last%20commit&color=purple)
[![Followers](https://img.shields.io/github/followers/D4rk-Pho3nix?style=flat-square&logo=github&color=yellow)](https://github.com/D4rk-Pho3nix)
![License](https://img.shields.io/github/license/D4rk-Pho3nix/OpenSauce?style=flat-square&color=orange)
[![Contact](https://img.shields.io/badge/Contact-Dev-cyan?style=flat-square)](mailto:manish.srmist23@gmail.com)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/D4rk-Pho3nix/OpenSauce/blob/main/Audio8_ASR_Infinite.ipynb)

A minimal Jupyter notebook that transcribes an audio file to text with the HF model [Edge0/Audio8-ASR-Infinite](https://huggingface.co/Edge0/Audio8-ASR-Infinite) in Chinese or English.

**made with 🩷 by [D4rk-Pho3nix](https://github.com/D4rk-Pho3nix)**

*(if you like my work, consider ⭐ starring the repo!)*

</div>

## Table of Contents

- [💡 Why this exists](#-why-this-exists)
- [✨ Features](#-features)
- [🏗️ Architecture](#️-architecture)
- [🚀 Quick Start](#-quick-start)
- [📖 Usage](#-usage)
- [🎗️ Maintainers](#️-maintainers)
- [🩷 Contributors](#-contributors)
- [💖 Support](#-support)
- [📄 License](#-license)

## 💡 Why this exists

Audio8 ASR Infinite is not a drop-in `pipeline("automatic-speech-recognition")` model. It pairs a streaming audio tower with a Qwen decoder and needs a dedicated decoding loop, so the snippet Hugging Face generates for it does not work.

This repository is a short, reproducible notebook that does the working setup for you: load the model from the Hub and turn spoken audio into text.

## ✨ Features

- Loads the model directly from the Hugging Face Hub (no manual download or clone).
- Transcribes an audio file (wav, mp3, flac and other formats `librosa` can read) in Chinese or English.
- Selectable transcription delay (`TARGET_DELAY_MS`) to trade latency for accuracy.
- Runs in Google Colab or locally, on GPU or CPU.
- One short notebook, no servers and no extra framework.

**Limitations**

- Audio is decoded as *simulated streaming* from a file. There is no microphone or real-time input here.
- Keep clips to about 30 seconds, the model's native context.
- The first run downloads about 8 GB of weights.
- The model's 24/7 unlimited-length mode needs the authors' vLLM setup, which is not part of this repository.
- Colab's free T4 GPU has no native bfloat16, so the notebook uses float16 there. That path has not been tested.

## 🏗️ Architecture

```text
OpenSauce/
├── Audio8_ASR_Infinite.ipynb   # the ASR demo notebook
├── requirements.txt            # dependencies for running locally
├── README.md
└── Audio8-ASR-Infinite/        # optional local clone of the model repo (not used by the notebook)
```

How the notebook works:

1. Install the `audio8-asr-infinite` package, which provides the model code and streaming decoder.
2. Load the tokenizer, feature extractor and model from `Edge0/Audio8-ASR-Infinite`.
3. Load the audio as 16 kHz mono.
4. Run `simulated_streaming_greedy_decode_batch` and print the text.

## 🚀 Quick Start

```bash
git clone https://github.com/D4rk-Pho3nix/OpenSauce.git
cd OpenSauce
```

**Google Colab (recommended)**

1. Open [`Audio8_ASR_Infinite.ipynb`](Audio8_ASR_Infinite.ipynb) in Colab using the badge above.
2. Choose Runtime > Change runtime type > GPU.
3. Choose Runtime > Run all.

**Locally** (Python 3.11 or 3.12, `ffmpeg` on your PATH)

```bash
python -m venv .venv
.venv\Scripts\activate          # Windows
# source .venv/bin/activate     # macOS / Linux
pip install -r requirements.txt
jupyter lab
```

Then open `Audio8_ASR_Infinite.ipynb` and run all cells.

Hardware notes: the weights are about 8 GB in bfloat16. A GPU with 16 GB or more of memory is the smooth path. Without a large enough GPU the notebook falls back to CPU, which needs roughly 9 GB of free RAM and is slow.

## 📖 Usage

Run the cells in order. The notebook's default audio is the first 30 seconds of the model's own demo video, downloaded from the Hub.

To transcribe your own file, edit the audio cell:

```python
AUDIO_PATH = "my_recording.wav"   # wav, mp3 or flac
```

and delete the three lines above it that build `sample.wav` from the demo video. Set `LANGUAGE` to `"en"` or `"zh"` in the settings cell to match your audio.

Output:

```text
Transcription: <the transcribed text>
```

## 🎗️ Maintainers

- [D4rk-Pho3nix](https://github.com/D4rk-Pho3nix)

## 🩷 Contributors

- [D4rk-Pho3nix](https://github.com/D4rk-Pho3nix)
- [Varsha-Venkataraman](https://github.com/Varsha-Venkataraman)

## 💖 Support

If this saved you some time, you can support the work here:

[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-support-yellow?style=flat-square&logo=buymeacoffee)](https://buymeacoffee.com/d4rkpho3nix)

## 📄 License

The model ([Edge0/Audio8-ASR-Infinite](https://huggingface.co/Edge0/Audio8-ASR-Infinite)) and the [audio8-asr-infinite](https://github.com/Edge0-AI/Audio8-ASR-Infinite) package are each licensed by their authors under Apache-2.0.

<div align="center">

[⬆ Back to Top](#audio8-asr-infinite-speech-recognition-demo)

<br>

[![Star History Chart](https://api.star-history.com/svg?repos=D4rk-Pho3nix/OpenSauce&type=Date)](https://star-history.com/#D4rk-Pho3nix/OpenSauce&Date)

</div>
