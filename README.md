# 🖼️ Text-to-Image Generation with Stable Diffusion

A Google Colab notebook that generates images from text prompts using Stable Diffusion v1.5 and the Hugging Face `diffusers` library.

![Python](https://img.shields.io/badge/Python-3.x-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-red)
![Colab](https://img.shields.io/badge/Google-Colab-orange)

## ✨ Features

- Generates images from any text prompt
- Supports negative prompts to avoid blurry or distorted results
- Runs in half precision (`float16`) on GPU for speed and lower memory use
- Saves generated images and downloads them straight from Colab

## 🛠 Tech Stack

- Python, PyTorch
- Hugging Face `diffusers`, `transformers`, `accelerate`, `safetensors`
- Model: `stable-diffusion-v1-5`
- Google Colab (T4 GPU)

## ⚡ Getting Started

1. Open `imageToImage.ipynb` in Google Colab.
2. Go to `Runtime` → `Change runtime type` → select **T4 GPU**.
3. Run all cells.

Install command used in the notebook:

```bash
pip install -q diffusers transformers accelerate safetensors
```

## 🚀 Usage

Load the pipeline:

```python
import torch
from diffusers import StableDiffusionPipeline

pipe = StableDiffusionPipeline.from_pretrained(
    "stable-diffusion-v1-5/stable-diffusion-v1-5",
    torch_dtype=torch.float16
).to("cuda")
```

Generate an image:

```python
image = pipe(
    "a futuristic city at sunset, highly detailed, digital art",
    negative_prompt="blurry, low quality, distorted",
    num_inference_steps=30,
    guidance_scale=7.5
).images[0]
image.save("output.png")
```

Download it to your computer:

```python
from google.colab import files
files.download("output.png")
```

## 🎛 Parameters

| Parameter | Value used | Meaning |
|-----------|-----------|---------|
| `num_inference_steps` | 30 | More steps = more detail, slower |
| `guidance_scale` | 7.5 | How strongly the image follows the prompt |
| `negative_prompt` | blurry, low quality, distorted | What the model should avoid |

## 🖼 Example Prompts

- `a futuristic city at sunset, highly detailed, digital art`
- `a cute fluffy cat sitting on a sofa, realistic photo, highly detailed, soft lighting`
- `a cute cat wearing sunglasses, realistic photo`

## 🔄 Workflow

<img width="1817" height="391" alt="image" src="https://github.com/user-attachments/assets/0de0d04d-c0cd-40a5-a41b-5be7c18e3d3d" />


## ⚠️ Notes

- A GPU is required. The first run downloads about 5 GB of model files.
- Set an `HF_TOKEN` to avoid Hugging Face rate-limit warnings.
- Despite the notebook's file name, it performs **text-to-image** generation.

## 📄 License

MIT License
