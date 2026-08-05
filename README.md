# Awesome MiniMax-H3

A curated list of models, text encoders, quants, and tools for the MiniMax-H3 omni-modal video generation model.

<div align="center">

<img src="https://github.com/user-attachments/assets/0c373d38-4c80-4140-b17e-4cfc6aa281c7" />

[![Telegram][telegram-shield]][telegram-url]
[![X][x-shield]][x-url]

</div>

<details>
<summary><b>Table of Contents</b></summary>

* [Models](#models)
  * [Checkpoints](#checkpoints)
  * [Quantized Models](#quants)
* [Text Encoders](#text-encoder)
* [Separated Components](#components)
  * [VAE (Video & Audio)](#components-vae)
  * [Tiny Autoencoder (TAE)](#tae)
* [LoRA](#lora)
  * [Styles](#lora)
* [ComfyUI Nodes](#nodes)
  * [Custom Node Collections](#nodes)
* [Guides & Tutorials](#guides)
* [Workflow & Technical Notes](#wf)
  * [ComfyUI](#wf-comfyui)

</details>

<a id="intro"></a>

## Intro

* [MiniMax-H3 official model card](https://huggingface.co/MiniMaxAI/MiniMax-H3)
* ComfyUI official [blogpost](https://blog.comfy.org/p/minimax-h3-day-0-support-in-comfyui)
* [ComfyUI tutorials for MiniMax-H3](https://docs.comfy.org/tutorials/video/minimax/minimax-h3)
* [Video Prompt Writing Guide (Base)](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/docs/VIDEO_PROMPT_WRITING_GUIDE_base_en.md)
* [Video Prompt Writing Guide (Reference)](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/docs/VIDEO_PROMPT_WRITING_GUIDE_ref_en.md)

<a id="models"></a>

## ▓ Models

MiniMax-H3 is a general-purpose, omni-modal generative system by [MiniMaxAI](https://huggingface.co/MiniMaxAI/MiniMax-H3). It supports unified understanding of multimodal contexts composed of text, images, video, and audio, and can generate video with native stereo audio at resolutions up to 2K and durations of up to 15 seconds. The model has two variants: **FL2VA** (first-and-last-frame mode) and **Ref2VA** (omni-reference mode).

<a id="checkpoints"></a>

### ▣ Checkpoints

Official and ComfyUI-repackaged model files.

* **[MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3)** - Official repository.
* **[Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3)** - ComfyUI-repackaged model files.

| Variant | Name | Precision | Size | Download |
| :--- | :--- | :---: | :---: | :---: |
| FL2VA | `minimax_h3_fl2va` | ![bf16][badge-bf16] | 61.73 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_fl2va_bf16.safetensors) |
| FL2VA | `minimax_h3_fl2va` | ![int8][badge-int8] | 31.70 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_fl2va_int8_convrot.safetensors) |
| FL2VA | `minimax_h3_fl2va_pruned` | ![bf16][badge-bf16] | 37.46 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_fl2va_pruned_bf16.safetensors) |
| FL2VA | `minimax_h3_fl2va_pruned` | ![fp8][badge-fp8] | 19.52 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_fl2va_pruned_fp8_scaled.safetensors) |
| FL2VA | `minimax_h3_fl2va_pruned` | ![int8][badge-int8] | 19.53 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_fl2va_pruned_int8_convrot.safetensors) |
| Ref2VA | `minimax_h3_ref2va` | ![bf16][badge-bf16] | 61.73 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_ref2va_bf16.safetensors) |
| Ref2VA | `minimax_h3_ref2va` | ![int8][badge-int8] | 31.70 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_ref2va_int8_convrot.safetensors) |
| Ref2VA | `minimax_h3_ref2va_pruned` | ![bf16][badge-bf16] | 37.46 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_ref2va_pruned_bf16.safetensors) |
| Ref2VA | `minimax_h3_ref2va_pruned` | ![fp8][badge-fp8] | 19.52 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_ref2va_pruned_fp8_scaled.safetensors) |
| Ref2VA | `minimax_h3_ref2va_pruned` | ![int8][badge-int8] | 19.53 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_ref2va_pruned_int8_convrot.safetensors) |

**Model Variants:**
- **H3-Base-FL2VA** (First-and-last-frame mode): Supports zero, one, or two input images. No image input = T2V; one image = first/last-frame-to-video; two images = first-and-last-frame-to-video.
- **H3-Base-Ref2VA** (Omni-reference mode): Supports multi-modal reference inputs — up to 9 images, 3 video clips (2–15s each), 3 audio clips, max 12 files total.

<p id="quants" align="center">══════════════════════════════════</p>

### ▣ Quantized Models

Community quantizations for lower memory usage. In ComfyUI, these are typically loaded as transformer-only models.

#### [Abiray/MiniMax-H3-GGUF](https://huggingface.co/Abiray/MiniMax-H3-GGUF)

GGUF quantized versions of both FL2VA and Ref2VA base models. Includes text encoder and VAE files.

<details>
<summary>FL2VA GGUF</summary>

| Model | Quant | Size | Download |
| :--- | :---: | :---: | :--- |
| FL2VA | ![Q3_K_M][badge-Q3_K_M] | 14.50 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-FL2VA-Q3_K_M.gguf) |
| FL2VA | ![Q3_K_S][badge-Q3_K_S] | 14.50 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-FL2VA-Q3_K_S.gguf) |
| FL2VA | ![Q4_0][badge-Q4_0] | 17.36 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-FL2VA-Q4_0.gguf) |
| FL2VA | ![Q4_K_M][badge-Q4_K_M] | 18.50 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-FL2VA-Q4_K_M.gguf) |
| FL2VA | ![Q4_K_S][badge-Q4_K_S] | 18.49 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-FL2VA-Q4_K_S.gguf) |
| FL2VA | ![Q5_0][badge-Q5_0] | 21.21 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-FL2VA-Q5_0.gguf) |
| FL2VA | ![Q5_K_M][badge-Q5_K_M] | 22.25 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-FL2VA-Q5_K_M.gguf) |
| FL2VA | ![Q5_K_S][badge-Q5_K_S] | 22.25 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-FL2VA-Q5_K_S.gguf) |

</details>

<details>
<summary>Ref2VA GGUF</summary>

| Model | Quant | Size | Download |
| :--- | :---: | :---: | :--- |
| Ref2VA | ![Q3_K_M][badge-Q3_K_M] | 14.50 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-Ref2VA-Q3_K_M.gguf) |
| Ref2VA | ![Q3_K_S][badge-Q3_K_S] | 14.50 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-Ref2VA-Q3_K_S.gguf) |
| Ref2VA | ![Q4_0][badge-Q4_0] | 17.36 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-Ref2VA-Q4_0.gguf) |
| Ref2VA | ![Q4_K_S][badge-Q4_K_S] | 18.49 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-Ref2VA-Q4_K_S.gguf) |
| Ref2VA | ![Q5_0][badge-Q5_0] | 21.21 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-Ref2VA-Q5_0.gguf) |
| Ref2VA | ![Q5_K_M][badge-Q5_K_M] | 22.25 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-Ref2VA-Q5_K_M.gguf) |
| Ref2VA | ![Q5_K_S][badge-Q5_K_S] | 22.25 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-Ref2VA-Q5_K_S.gguf) |

</details>

#### [realrebelai/MiniMax-H3_GGUFs](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs)

GGUF quantized versions of FL2VA and Ref2VA. Includes text encoder GGUFs and workflow JSONs.

| Model | Quant | Size | Download |
| :--- | :---: | :---: | :--- |
| FL2VA | ![Q2_K][badge-Q2_K] | 17.42 GB | [![][gh-realrebelai]](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs/resolve/main/MiniMax-H3-FL2VA-Q2_K-(Mixed_Precision).gguf) |
| FL2VA | ![Q3_K_M][badge-Q3_K_M] | 14.51 GB | [![][gh-realrebelai]](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs/resolve/main/MiniMax-H3-FL2VA-Q3_K_M.gguf) |
| FL2VA | ![Q4_K_M][badge-Q4_K_M] | 18.50 GB | [![][gh-realrebelai]](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs/resolve/main/MiniMax-H3-FL2VA-Q4_K_M.gguf) |
| Ref2VA | ![Q3_K_M][badge-Q3_K_M] | 14.51 GB | [![][gh-realrebelai]](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs/resolve/main/MiniMax-H3-REF2VA-Q3_K_M.gguf) |
| Ref2VA | ![Q4_K_M][badge-Q4_K_M] | 18.50 GB | [![][gh-realrebelai]](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs/resolve/main/MiniMax-H3-REF2VA-Q4_K_M.gguf) |

#### [rockerBOO/minimax-h3-nvfp4](https://huggingface.co/rockerBOO/minimax-h3-nvfp4)

NVFP4 quantized versions of the MiniMax H3 diffusion transformer. Includes pruned (AdaLN-pruned for ComfyUI) and experimental INT4 ConvRot variants.

| Model | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| FL2VA | ![nvfp4][badge-nvfp4] | 32.05 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_fl2va_nvfp4.safetensors) |
| FL2VA (pruned) | ![nvfp4][badge-nvfp4] | 18.69 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_fl2va_pruned_nvfp4.safetensors) |
| FL2VA (pruned + ConvRot INT8) | ![nvfp4][badge-nvfp4] | 18.69 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_fl2va_pruned_nvfp4_convrot_int8.safetensors) |
| FL2VA (INT4 ConvRot, experimental) | ![int4][badge-int4] | 23.60 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_fl2va_int4_convrot_simple.safetensors) |
| FL2VA (pruned INT4 ConvRot, experimental) | ![int4][badge-int4] | 15.67 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_fl2va_pruned_int4_convrot_simple.safetensors) |
| FL2VA (pruned mixed INT4/INT8 ConvRot, experimental) | ![int4][badge-int4] | 18.92 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_fl2va_pruned_mixed_int4_int8_convrot_simple.safetensors) |
| Ref2VA | ![nvfp4][badge-nvfp4] | 32.05 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_ref2va_nvfp4.safetensors) |
| Ref2VA (pruned) | ![nvfp4][badge-nvfp4] | 18.69 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_ref2va_pruned_nvfp4.safetensors) |
| Ref2VA (pruned + ConvRot INT8) | ![nvfp4][badge-nvfp4] | 18.69 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_ref2va_pruned_nvfp4_convrot_int8.safetensors) |

#### [rzgar/minimax_h3_fl2va_fp8_e4m3fn](https://huggingface.co/rzgar/minimax_h3_fl2va_fp8_e4m3fn)

FP8 (E4M3FN), MXFP8, and FP16-attention quantized versions of the FL2VA diffusion transformer. MXFP8 offers better audio at 5 and 8 steps; FP16attn balances quality and performance.

| Model | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| FL2VA | ![fp8][badge-fp8] | 43.78 GB | [![][gh-rzgar]](https://huggingface.co/rzgar/minimax_h3_fl2va_fp8_e4m3fn/resolve/main/minimax_h3_fl2va_fp8_e4m3fn.safetensors) |
| FL2VA | ![mxfp8][badge-mxfp8] | 44.34 GB | [![][gh-rzgar]](https://huggingface.co/rzgar/minimax_h3_fl2va_fp8_e4m3fn/resolve/main/minimax_h3_fl2va_mxfp8.safetensors) |
| FL2VA (FP16 attention) | ![fp8][badge-fp8] | 26.70 GB | [![][gh-rzgar]](https://huggingface.co/rzgar/minimax_h3_fl2va_fp8_e4m3fn/resolve/main/minimax_h3_fl2va_fp16attn_fp8.safetensors) |

#### [DiffSynth-Studio/MiniMax-H3-NF4](https://huggingface.co/DiffSynth-Studio/MiniMax-H3-NF4)

NF4 (bitsandbytes 4-bit) quantized version designed for use with [DiffSynth-Studio](https://github.com/modelscope/DiffSynth-Studio). Minimum 8GB VRAM required.

| Model | Size | Download |
| :--- | :---: | :--- |
| FL2VA NF4 | 15.98 GB | [![][gh-DiffSynth-Studio]](https://huggingface.co/DiffSynth-Studio/MiniMax-H3-NF4/resolve/main/minimax-h3-fl2va-nf4.safetensors) |
| Ref2VA NF4 | 15.98 GB | [![][gh-DiffSynth-Studio]](https://huggingface.co/DiffSynth-Studio/MiniMax-H3-NF4/resolve/main/minimax-h3-ref2va-nf4.safetensors) |
| Text Encoder NF4 | 14.27 GB | [![][gh-DiffSynth-Studio]](https://huggingface.co/DiffSynth-Studio/MiniMax-H3-NF4/resolve/main/minimax-h3-text-encoder-nf4.safetensors) |
| Video VAE NF4 | 1.50 GB | [![][gh-DiffSynth-Studio]](https://huggingface.co/DiffSynth-Studio/MiniMax-H3-NF4/resolve/main/video_vae_nf4.safetensors) |
| Audio VAE NF4 | 271 MB | [![][gh-DiffSynth-Studio]](https://huggingface.co/DiffSynth-Studio/MiniMax-H3-NF4/resolve/main/audio_vae_nf4.safetensors) |

#### [WaveCut/MiniMax-H3-OrbitQuant-W4A4](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4)

Native OrbitQuant W4A4 conversion. Eligible linear weights in `transformer`, `transformer_ref`, and the Qwen3-VL `text_encoder` are stored and executed through OrbitQuant's native packed W4A4 path. BF16 is the compute dtype for non-quantized modules. Visual and audio VAEs are byte-for-byte FP32 source copies.

| Component | Size | Download |
| :--- | :---: | :--- |
| Transformer (FL2VA) | 17.03 GB | [![][gh-WaveCut]](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/transformer/diffusion_pytorch_model-00001-of-00005.safetensors) |
| Transformer Ref (Ref2VA) | 17.03 GB | [![][gh-WaveCut]](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/transformer_ref/diffusion_pytorch_model-00001-of-00005.safetensors) |
| Text Encoder | 18.56 GB | [![][gh-WaveCut]](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/text_encoder/model-00001-of-00005.safetensors) |
| Video VAE (FP32) | 9.70 GB | [![][gh-WaveCut]](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/vae/diffusion_pytorch_model-00001-of-00003.safetensors) |
| Audio VAE (FP32) | 577 MB | [![][gh-WaveCut]](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/audio_vae/diffusion_pytorch_model.safetensors) |

*Requires [ComfyUI-OrbitQuant](https://github.com/iamwavecut/ComfyUI-OrbitQuant/tree/feature/minimax-h3-comfyui) custom node. See the repo for [ComfyUI workflow JSON](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/comfyui/workflows/MiniMax-H3-OrbitQuant-T2VA.json).*

#### [DmitryDB/MiniMax-H3-ComfyUI-Quants](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants)

Stock-compatible community quants — all files load in unmodified ComfyUI. Multiple quality tiers from INT8 ConvRot to W4 ConvRot to NVFP4, covering 8GB–32GB+ GPU classes.

| Model | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| FL2VA | ![int8][badge-int8] | 21.91 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/FL2VA/MiniMax-H3_FL2VA-INT8-ConvRot-HQ.safetensors) |
| FL2VA | ![int8][badge-int8] | 20.94 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/FL2VA/MiniMax-H3_FL2VA-INT8-ConvRot.safetensors) |
| FL2VA | ![int8][badge-int8] | 20.33 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/FL2VA/MiniMax-H3_FL2VA-INT8-ConvRot-Lite.safetensors) |
| FL2VA | ![nvfp4][badge-nvfp4] | 13.60 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/FL2VA/MiniMax-H3_FL2VA-NVFP4-HQ.safetensors) |
| FL2VA | ![nvfp4][badge-nvfp4] | 10.86 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/FL2VA/MiniMax-H3_FL2VA-NVFP4.safetensors) |
| FL2VA | ![int4][badge-int4] | 10.07 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/FL2VA/MiniMax-H3_FL2VA-W4-ConvRot.safetensors) |
| FL2VA | ![int4][badge-int4] | 9.71 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/FL2VA/MiniMax-H3_FL2VA-W4-ConvRot-Offload.safetensors) |
| FL2VA | ![int4][badge-int4] | 13.57 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/FL2VA/MiniMax-H3_FL2VA-W8W4-ConvRot.safetensors) |
| Ref2VA | ![int8][badge-int8] | 21.91 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/Ref2VA/MiniMax-H3_Ref2VA-INT8-ConvRot-HQ.safetensors) |
| Ref2VA | ![int8][badge-int8] | 20.94 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/Ref2VA/MiniMax-H3_Ref2VA-INT8-ConvRot.safetensors) |
| Ref2VA | ![int8][badge-int8] | 20.33 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/Ref2VA/MiniMax-H3_Ref2VA-INT8-ConvRot-Lite.safetensors) |
| Ref2VA | ![nvfp4][badge-nvfp4] | 13.60 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/Ref2VA/MiniMax-H3_Ref2VA-NVFP4-HQ.safetensors) |
| Ref2VA | ![nvfp4][badge-nvfp4] | 10.86 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/Ref2VA/MiniMax-H3_Ref2VA-NVFP4.safetensors) |
| Ref2VA | ![int4][badge-int4] | 10.07 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/Ref2VA/MiniMax-H3_Ref2VA-W4-ConvRot.safetensors) |
| Ref2VA | ![int4][badge-int4] | 9.71 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/Ref2VA/MiniMax-H3_Ref2VA-W4-ConvRot-Offload.safetensors) |
| Ref2VA | ![int4][badge-int4] | 13.57 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/Ref2VA/MiniMax-H3_Ref2VA-W8W4-ConvRot.safetensors) |

#### [DmitryDB/MiniMax-H3-DynTime-sQKV](https://huggingface.co/DmitryDB/MiniMax-H3-DynTime-sQKV)

Experimental dynamic-time, physically separate Q/K/V editions. **Requires a ComfyUI core patch** — does not load in unmodified ComfyUI. Retains the original FP32 time MLP and physically separate Q, K, V projections.

| Model | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| FL2VA | ![int8][badge-int8] | 21.00 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-DynTime-sQKV/resolve/main/FL2VA/MiniMax-H3_FL2VA-DT-sQKV-INT8-ConvRot.safetensors) |
| FL2VA (HQ) | ![int8][badge-int8] | 27.99 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-DynTime-sQKV/resolve/main/FL2VA/MiniMax-H3_FL2VA-DT-sQKV-INT8-ConvRot-HQ.safetensors) |
| Ref2VA | ![int8][badge-int8] | 21.00 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-DynTime-sQKV/resolve/main/Ref2VA/MiniMax-H3_Ref2VA-DT-sQKV-INT8-ConvRot.safetensors) |
| Ref2VA (HQ) | ![int8][badge-int8] | 27.99 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-DynTime-sQKV/resolve/main/Ref2VA/MiniMax-H3_Ref2VA-DT-sQKV-INT8-ConvRot-HQ.safetensors) |

#### [DmitryDB/MiniMax-H3-INT8-Lean-ConvRot](https://huggingface.co/DmitryDB/MiniMax-H3-INT8-Lean-ConvRot)

Quality-oriented mixed-precision INT8 ConvRot conversions. Stock-compatible — loads in unmodified ComfyUI. The quality21 policy keeps high-risk matrices in BF16 and compresses the rest (170 INT8 ConvRot + 30 BF16 main matrices).

| Model | Size | Download |
| :--- | :---: | :--- |
| FL2VA INT8 Lean ConvRot | 20.94 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-INT8-Lean-ConvRot/resolve/main/FL2VA/minimax-h3-fl2va-int8-lean-convrot-table-k16-g4097-quality21.safetensors) |
| Ref2VA INT8 Lean ConvRot | 20.94 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-INT8-Lean-ConvRot/resolve/main/Ref2VA/minimax-h3-ref2va-int8-lean-convrot-table-k16-g4097-quality21.safetensors) |

#### [DmitryDB/MiniMax-H3-INT8-Lean-ConvRot-Dynamic-Time-Separate-QKV](https://huggingface.co/DmitryDB/MiniMax-H3-INT8-Lean-ConvRot-Dynamic-Time-Separate-QKV)

Experimental edition with original FP32 time MLP and physically separate Q/K/V projections. **Requires a ComfyUI core patch** — does not load in unmodified ComfyUI.

| Model | Size | Download |
| :--- | :---: | :--- |
| FL2VA INT8 Lean ConvRot (Dynamic/Separate QKV) | 21.00 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-INT8-Lean-ConvRot-Dynamic-Time-Separate-QKV/resolve/main/FL2VA/minimax-h3-fl2va-int8-lean-convrot-dynamic-k16-separate-qkv-quality21.safetensors) |
| Ref2VA INT8 Lean ConvRot (Dynamic/Separate QKV) | 21.00 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-INT8-Lean-ConvRot-Dynamic-Time-Separate-QKV/resolve/main/Ref2VA/minimax-h3-ref2va-int8-lean-convrot-dynamic-k16-separate-qkv-quality21.safetensors) |

#### [tsolful/Minimax_H3_INT4MixedConvRot](https://huggingface.co/tsolful/Minimax_H3_INT4MixedConvRot)

Mixed INT4/INT8 ConvRot quants with two quality tiers: INT4Q (quality-leaning, ~73% INT8) and INT4BQ (balanced-quality, ~41% INT8).

| Model | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| FL2VA (INT4Q Quality) | ![int4][badge-int4] | 17.27 GB | [![][gh-tsolful]](https://huggingface.co/tsolful/Minimax_H3_INT4MixedConvRot/resolve/main/minimax_h3_fl2va_pruned_INT4Q.safetensors) |
| FL2VA (INT4BQ Balanced) | ![int4][badge-int4] | 14.81 GB | [![][gh-tsolful]](https://huggingface.co/tsolful/Minimax_H3_INT4MixedConvRot/resolve/main/minimax_h3_fl2va_pruned_INT4BQ.safetensors) |
| Ref2VA (INT4Q Quality) | ![int4][badge-int4] | 17.18 GB | [![][gh-tsolful]](https://huggingface.co/tsolful/Minimax_H3_INT4MixedConvRot/resolve/main/minimax_h3_ref2va_pruned_INT4Q.safetensors) |
| Ref2VA (INT4BQ Balanced) | ![int4][badge-int4] | 14.06 GB | [![][gh-tsolful]](https://huggingface.co/tsolful/Minimax_H3_INT4MixedConvRot/resolve/main/minimax_h3_ref2va_pruned_INT4BQ.safetensors) |

#### [AX1Y2JP/MiniMax-H3-W4A8-ConvRot](https://huggingface.co/AX1Y2JP/MiniMax-H3-W4A8-ConvRot)

Symmetric W4A8 ConvRot quantization — calibration-free 4-bit weight storage that runs on int8 GEMM with ConvRot activations. Requires a [comfy-kitchen PR #90](https://github.com/Comfy-Org/comfy-kitchen/pull/90) branch and custom nodes from the repo.

| Model | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| FL2VA (pruned) | ![int4][badge-int4] | 11.68 GB | [![][gh-AX1Y2JP]](https://huggingface.co/AX1Y2JP/MiniMax-H3-W4A8-ConvRot/resolve/main/minimax_h3_fl2va_pruned_symw4a8convrot.safetensors) |
| Ref2VA (pruned) | ![int4][badge-int4] | 11.68 GB | [![][gh-AX1Y2JP]](https://huggingface.co/AX1Y2JP/MiniMax-H3-W4A8-ConvRot/resolve/main/minimax_h3_ref2va_pruned_symw4a8convrot.safetensors) |

#### [Kijai/MiniMax-H3-experimental](https://huggingface.co/Kijai/MiniMax-H3-experimental)

Experimental W4A8 mixed-precision quant. Test model for the [comfy-kitchen PR #90](https://github.com/Comfy-Org/comfy-kitchen/pull/90) — calibration-free 4-bit weight storage with int8 codebook, dequantized to grouped int8 and fed to the int8 CUTLASS GEMM. ~0.073 weight relL2 (NVFP4 ~0.094), ~0.56 B/elem, ~1.09× int8 speed.

| Model | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| FL2VA (pruned W4A8 mixed) | ![int4][badge-int4] | 11.68 GB | [![][gh-Kijai]](https://huggingface.co/Kijai/MiniMax-H3-experimental/resolve/main/minimax_h3_fl2va_pruned_w4a8_mixed.safetensors) |

#### [Winnougan/MiniMax-H3-INT4_Convrot_ComfyUI](https://huggingface.co/Winnougan/MiniMax-H3-INT4_Convrot_ComfyUI)

INT4 ConvRot quantization for ComfyUI. Repository currently contains documentation only.

<p id="text-encoder" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ Text Encoders

MiniMax-H3 uses the Qwen3-VL-32B model as its text/vision conditioning encoder.

### ▣ Comfy-Org Optimized Encoders

Official and optimized versions for ComfyUI, repackaged by [Comfy-Org](https://huggingface.co/Comfy-Org/MiniMax-H3).

| Model Name | Precision | Size | Download |
| :--- | :---: | :---: | :---: |
| `qwen3vl_32b_minimax_h3` | ![bf16][badge-bf16] | 47.97 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/text_encoders/qwen3vl_32b_minimax_h3_bf16.safetensors) |
| `qwen3vl_32b_minimax_h3` | ![int8][badge-int8] | 25.28 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/text_encoders/qwen3vl_32b_minimax_h3_int8_convrot.safetensors) |
| `qwen3vl_32b_minimax_h3` | ![nvfp4][badge-nvfp4] | 14.61 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/text_encoders/qwen3vl_32b_minimax_h3_nvfp4_awq.safetensors) |

### ▣ Abiray GGUF Text Encoder

GGUF quantized text encoder, bundled with the [Abiray/MiniMax-H3-GGUF](https://huggingface.co/Abiray/MiniMax-H3-GGUF) repository.

| Model Name | Precision | Size | Download |
| :--- | :---: | :---: | :---: |
| `qwen3vl_32b_minimax_h3` | ![Q4_K_M][badge-Q4_K_M] | 13.58 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/text_encoders/qwen3vl_32b_minimax_h3-Q4_K_M.gguf) |
| `qwen3vl_32b_minimax_h3` | ![int4][badge-int4] | 13.93 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/text_encoders/qwen3vl_32b_minimax_h3_int4_convrot.safetensors) |
| `qwen3vl_32b_minimax_h3` | ![nvfp4][badge-nvfp4] | 25.28 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/text_encoders/qwen3vl_32b_minimax_h3_nvfp4_awq.safetensors) |

<p id="enc-heretic" align="center">· · · · · · · · · · · · · ·</p>

### ▣ Qwen3-VL-32B Ultra-Heretic (Uncensored)

Built from [`llmfan46/Qwen3-VL-32B-Instruct-ultra-uncensored-heretic`](https://huggingface.co/llmfan46/Qwen3-VL-32B-Instruct-ultra-uncensored-heretic) by [ethanfel](https://huggingface.co/ethanfel). Includes a MiniMax-H3 conditioning encoder (language layers 0–49 + vision tower) and an optional prompt-enhancement tail (layers 50–63 + LM head). The "Heretic" lineage bypasses alignment/restriction layers in the text encoder so MiniMax-H3 receives the most faithful prompt embeddings.

| Model Name | Precision | Size | Download |
| :--- | :---: | :---: | :---: |
| `qwen3vl_32b_heretic` (conditioning encoder) | ![int8][badge-int8] | 24.55 GB | [![][gh-ethanfel]](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-MiniMax-H3-ComfyUI-INT8-ConvRot/resolve/main/qwen3vl_32b_minimax_h3_ultra_uncensored_heretic_int8_convrot.safetensors) |
| `qwen3vl_32b_heretic` (generation tail 50–63) | ![int8][badge-int8] | 7.09 GB | [![][gh-ethanfel]](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-MiniMax-H3-ComfyUI-INT8-ConvRot/resolve/main/qwen3vl_32b_minimax_h3_generation_tail_50_63_int8_convrot.safetensors) |

*The generation tail is loaded temporarily by the [ComfyUI-MiniMax-H3-Guide](https://github.com/ethanfel/ComfyUI-MiniMax-H3-Guide) node for prompt enhancement, then unloaded. Requires the connected standard MiniMax-H3 CLIP (layers 0–49).*


<p id="components" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ Separated Components

Separated VAE files for MiniMax-H3. The video VAE and audio VAE are required for all generation workflows.

<a id="components-vae"></a>

### ▣ VAE (Video & Audio)

| Component | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| Video VAE | ![fp16][badge-fp16] | 4.85 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/vae/minimax_h3_video_vae_fp16.safetensors) |
| Audio VAE | fp32 | 577 MB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/vae/minimax_h3_audio_vae_fp32.safetensors) |

#### FP8 VAE (dummy9996)

FP8-mixed quantized video VAE by [dummy9996](https://huggingface.co/dummy9996/minimax_h3_vae_fp8).

| Component | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| Video VAE | ![fp8][badge-fp8] | 2.60 GB | [![][gh-dummy9996]](https://huggingface.co/dummy9996/minimax_h3_vae_fp8/resolve/main/minimax_h3_video_vae_fp8mix.safetensors) |
| Audio VAE | ![bf16][badge-bf16] | 289 MB | [![][gh-dummy9996]](https://huggingface.co/dummy9996/minimax_h3_vae_fp8/resolve/main/minimax_h3_audio_vae_bf16.safetensors) |

<p id="tae" align="center">· · · · · · · · · · · · · ·</p>

### ▣ Tiny Autoencoder (TAE)

Quickly trained 2D tiny VAE for MiniMax-H3 by [Kijai](https://huggingface.co/Kijai/MiniMax-H3-TAE). Not the greatest outcome, still beats latent2rgb for preview purposes. Currently only works with the `ModelPreviewOverride` node in [ComfyUI-KJNodes](https://github.com/kijai/ComfyUI-KJNodes).

| Component | Size | Download |
| :--- | :---: | :--- |
| TAE (preview VAE) | 9 MB | [![][gh-Kijai]](https://huggingface.co/Kijai/MiniMax-H3-TAE/resolve/main/vae_approx/taeh3.safetensors) |


<p id="lora" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ LoRA

### ▣ Styles

* SexGod1979
  * [PinkFluffyBunny](https://huggingface.co/SexGod1979/PinkFluffyBunny-MiniMax-H3) - Pink fluffy bunny style LoRA. Maximum pink achieved at 0.5 strength on pruned int8 model. Alpha quality. (2.31 GB)
  * [NaughtyTimes](https://huggingface.co/SexGod1979/NaughtyTimes_MiniMax-H3) - NSFW style LoRA for MiniMax-H3.

* ssjenforcer191
  * [Homelander](https://huggingface.co/ssjenforcer191/Homelander_Minimax_H3_experimental) - Character LoRA for The Boys' Homelander. Triggerword `HeroHomelander` (optionally append `wearing red leather gloves`). Experimental. (296 MB)

<p id="nodes" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ ComfyUI Nodes

### ▣ Custom Node Collections

* [MiniMax H3 Hybrid Cond](https://github.com/kitsune123150/minimax-h3-hybrid-cond) by kitsune123150 - ComfyUI custom node for MiniMax H3 conditioning. Supports both reference-to-video (`ref2va` / R2V) and first/last-frame video conditioning (`fl2va` / I2V), including a hybrid mode that uses both in one conditioning payload. Required model inputs are the H3 video VAE, H3 audio VAE, and the matching H3 CLIP/text encoder. The node outputs a positive conditioning and an AV latent with native audio.

* [MiniMaxH3 LatentUpscaler](https://github.com/Tr1dae/ComfyUI-MiniMaxH3_LatentUpscaler) by Tr1dae - ComfyUI custom node for latent spatial upscaling between MiniMax H3 samplers. Not a learned AI upscaler — handles the stock `LatentUpscaleBy` / `AddNoise` breakage on MiniMax's ComfyUI `NestedTensor` AV latents (`video [B,24,T,H/16,W/16]` + `audio [B,32,2,T_audio]`). Upscales video H/W via `F.interpolate`, re-noises video at `sigmas[0]`, and optionally re-noises audio for pass-2 polish. Also spatially upscales `minimax_refs` / `minimax_keyframes` visual latents and syncs `latent_h` / `latent_w`.

* [ComfyUI-SolAttn_triton](https://github.com/kijai/ComfyUI-SolAttn_triton) by kijai - SolAttention triton kernel implementation for ComfyUI. Provides optimized attention computation for MiniMax-H3 and other models using the SolAttention mechanism.

* [ComfyUI-sol-attn](https://github.com/Saganaki22/ComfyUI-sol-attn) by Saganaki22 - NVIDIA Sol-Attn Triton kernel for SM89/SM90/SM100/SM120 with zero-copy MiniMax H3 nodes: memory-efficient attention, scheduled tau with graph preview, and feed-forward chunking. Measured 1.14–1.44× vs SageAttention and −37% MLP peak VRAM on H3. Vendored NVIDIA Apache-2.0 kernel with SM120 (RTX 50-series) enablement.

* [ComfyUI Spectrum MiniMax H3](https://github.com/xmarre/ComfyUI-Spectrum-MiniMax-H3) by xmarre - Spectrum-based acceleration for ComfyUI's native MiniMax H3 audio-video model. Forecasts post-transformer features with Chebyshev ridge regression to skip selected transformer evaluations, with adaptive scheduling, sampler-aware safeguards, CPU/VRAM history storage, and native fallbacks. Reduces expensive H3 transformer evaluations during sampling.

* [ComfyUI-H3-Multishot](https://github.com/jlucasmcrell/ComfyUI-H3-Multishot) by jlucasmcrell - Multishot video+audio generation for MiniMax-H3 in ComfyUI: one script, N chained shots, one seam-clean master. Includes a dual-format model loader (safetensors + GGUF), keyframes at any position (not just first/last), condition strength control, and stereo audio guard for reference clips.

* [ComfyUI MiniMax H3 Image Studio](https://github.com/astropuzzo/ComfyUI-MiniMax-H3-Image-Studio) by astropuzzo - Image-first ComfyUI nodes for using MiniMax H3 as a text-to-image, image-to-image, and reference-edit generator. Provides image-oriented conditioning, arbitrary frame counts, resolution controls up to 64 MP, automatic still-frame scoring, and single-image output.

* [ComfyUI MiniMax H3 Director](https://github.com/seesee75-commits/ComfyUI-MiniMaxH3-Director) by seesee75-commits - Timeline editor for MiniMax H3 inside ComfyUI. Drag images, videos and music onto tracks, trim them on a ruler, write a prompt per shot, press Run. Storyboard-based approach with live sampling preview, retakes, and shot chaining. Ported from the LTX Director by WhatDreamsCost.

* [ComfyUI Fantastic MiniMax H3 Prompt Builder](https://github.com/Adudeguyman/ComfyUI-Fantastic-MiniMaxH3-PromptBuilder) by Adudeguyman - Guided prompt writing and reference-media handling for MiniMax H3. Fillable templates for every prompt mode, live checking against the official guide's rules, and a media loader that keeps reference tags straight. Three nodes: Prompt Builder, Media Loader, and Reference Splitter.

* [ComfyUI MiniMax-H3 Prompt Enhancer T8](https://github.com/T8mars/comfyui-minimax-h3-prompt-enhancer-T8) by T8mars - Prompt enhancer node for MiniMax-H3 video generation. Calls `bytedance/doubao-seed-evolving` to analyze text, images, and video together, outputting a structured prompt string. Supports T2VA, I2VA, FL2VA, L2VA, Ref2VA with strict/balanced/creative modes and Chinese/English output.

* [minimax-h3-mlx](https://github.com/mrbizarro/minimax-h3-mlx) by mrbizarro - MLX (Apple Silicon) port of MiniMax-H3 — 33B joint video+audio diffusion. Validated against the diffusers reference. AdaLN precompute drops 13B of parameters at inference. From-scratch MLX implementation of the full pipeline (not `mlx_lm.convert`).


<p id="guides" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ Guides & Tutorials

### ▣ Official Guides

* [Video Prompt Writing Guide (Base)](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/docs/VIDEO_PROMPT_WRITING_GUIDE_base_en.md) - Official MiniMax-H3 prompt writing guide for base (FL2VA) mode. Covers prompt structure, camera language, scene composition, and best practices for text-to-video and image-to-video generation.
* [Video Prompt Writing Guide (Reference)](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/docs/VIDEO_PROMPT_WRITING_GUIDE_ref_en.md) - Official MiniMax-H3 prompt writing guide for reference (Ref2VA) mode. Covers multi-modal reference inputs, image/video/audio reference handling, and prompt construction for omni-reference generation.

### ▣ ComfyUI Tutorials

* [ComfyUI MiniMax-H3 Tutorial](https://docs.comfy.org/tutorials/video/minimax/minimax-h3) - Official ComfyUI documentation tutorial for MiniMax-H3 setup and usage.
* [MiniMax H3 Day-0 Support in ComfyUI](https://blog.comfy.org/p/minimax-h3-day-0-support-in-comfyui) - ComfyUI blog post covering open weights, native audio, 2K video output, and local execution on a 3060.


<p id="wf" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ Workflow & Technical Notes

<a id="wf-comfyui"></a>

### ❖ ComfyUI

Official ComfyUI workflow templates for MiniMax-H3:

* [Text-to-Video (T2V)](https://github.com/Comfy-Org/workflow_templates/blob/main/templates/video_minimax_h3_t2v.json)
* [Image-to-Video (I2V)](https://github.com/Comfy-Org/workflow_templates/blob/main/templates/video_minimax_h3_i2v.json)
* [Reference-to-Video (R2V)](https://github.com/Comfy-Org/workflow_templates/blob/main/templates/video_minimax_h3_r2v.json)

### ❖ OrbitQuant

* [OrbitQuant T2VA Workflow](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/comfyui/workflows/MiniMax-H3-OrbitQuant-T2VA.json) - Ready-to-import ComfyUI workflow for the OrbitQuant W4A4 quantization. Derived from Comfy-Org's bundled T2V workflow.
* [OrbitQuant T2VA API Workflow](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/comfyui/workflows/MiniMax-H3-OrbitQuant-T2VA-api.json) - API prompt version of the T2VA workflow.
* [OrbitQuant Ref2VA API Workflow](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/comfyui/workflows/MiniMax-H3-OrbitQuant-Ref2VA-api.json) - API prompt version of the Ref2VA workflow.

### ❖ Abiray

* [MiniMax H3 FL2V GGUF Workflow](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/minimax_fl2v_gguf_workflow.json) - ComfyUI workflow for loading and running the GGUF quantized FL2VA model.

<!-- MARKDOWN LINKS & IMAGES -->
[telegram-shield]: https://img.shields.io/badge/TokenDiff-26A5E4?style=for-the-badge&logo=telegram&logoColor=white
[telegram-url]: https://t.me/TokenDiff
[x-shield]: https://img.shields.io/badge/wildmindai-000000?style=for-the-badge&logo=x&logoColor=white
[x-url]: https://x.com/wildmindai

[gh-Comfy--Org]: https://img.shields.io/badge/Comfy--Org-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-Abiray]: https://img.shields.io/badge/Abiray-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-DiffSynth-Studio]: https://img.shields.io/badge/DiffSynth--Studio-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-DmitryDB]: https://img.shields.io/badge/DmitryDB-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-WaveCut]: https://img.shields.io/badge/WaveCut-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-dummy9996]: https://img.shields.io/badge/dummy9996-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-ethanfel]: https://img.shields.io/badge/ethanfel-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-rockerBOO]: https://img.shields.io/badge/rockerBOO-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-Kijai]: https://img.shields.io/badge/Kijai-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-AX1Y2JP]: https://img.shields.io/badge/AX1Y2JP-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-tsolful]: https://img.shields.io/badge/tsolful-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-realrebelai]: https://img.shields.io/badge/realrebelai-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-rzgar]: https://img.shields.io/badge/rzgar-lightgrey?style=flat-square&logo=huggingface&logoColor=white

[badge-bf16]: https://img.shields.io/badge/bf16-0077cc?style=flat-square
[badge-fp16]: https://img.shields.io/badge/fp16-0077cc?style=flat-square
[badge-fp8]: https://img.shields.io/badge/fp8-28a745?style=flat-square
[badge-mxfp8]: https://img.shields.io/badge/mxfp8-20c997?style=flat-square
[badge-int8]: https://img.shields.io/badge/int8-17a2b8?style=flat-square
[badge-int4]: https://img.shields.io/badge/int4-ffc107?style=flat-square
[badge-nvfp4]: https://img.shields.io/badge/nvfp4-6f42c1?style=flat-square
[badge-Q2_K]: https://img.shields.io/badge/Q2__K-e05d44?style=flat-square
[badge-Q3_K_M]: https://img.shields.io/badge/Q3__K__M-fe7d37?style=flat-square
[badge-Q3_K_S]: https://img.shields.io/badge/Q3__K__S-fe7d37?style=flat-square
[badge-Q4_0]: https://img.shields.io/badge/Q4__0-dfb317?style=flat-square
[badge-Q4_K_M]: https://img.shields.io/badge/Q4__K__M-dfb317?style=flat-square
[badge-Q4_K_S]: https://img.shields.io/badge/Q4__K__S-dfb317?style=flat-square
[badge-Q5_0]: https://img.shields.io/badge/Q5__0-97c00f?style=flat-square
[badge-Q5_K_M]: https://img.shields.io/badge/Q5__K__M-97c00f?style=flat-square
[badge-Q5_K_S]: https://img.shields.io/badge/Q5__K__S-97c00f?style=flat-square
