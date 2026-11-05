# 🖼️ Image Generation With Pre-trained model

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

## 🎬Demo

<img width="640" height="640" alt="output_1_futuristic_city" src="https://github.com/user-attachments/assets/69a35cde-6a71-44eb-8a42-57f93c352599" />
<img width="640" height="640" alt="output_2_cat_on_sofa" src="https://github.com/user-attachments/assets/e5a6e5db-25b7-47da-8763-ba365d54c962" />
<img width="640" height="640" alt="output_3_cat_sunglasses" src="https://github.com/user-attachments/assets/c618406f-1725-40dc-9763-f1b23c07aa48" />


## 🔄 Workflow

<img width="1817" height="391" alt="image" src="https://github.com/user-attachments/assets/0de0d04d-c0cd-40a5-a41b-5be7c18e3d3d" />


## ⚠️ Notes

- A GPU is required. The first run downloads about 5 GB of model files.
- Set an `HF_TOKEN` to avoid Hugging Face rate-limit warnings.
- Despite the notebook's file name, it performs **text-to-image** generation.

## 📄 License

MIT License

## 👤 Author

**Samarth Nerurkar**

- GitHub: [@samarthnerurkar](https://github.com/samarthnerurkar)
- LinkedIn: [Samarth Nerurkar](https://www.linkedin.com/in/samarth-nerurkar/)
