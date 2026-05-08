# Free Image Generator

This repository contains a simple Jupyter notebook for generating AI images with Stable Diffusion. The notebook is designed to run in Google Colab, but it can also run locally on a machine with a compatible GPU.

The project uses Hugging Face Diffusers and the `stabilityai/stable-diffusion-2-1` model to generate images from text prompts.

## Project Structure

| File | Description |
| --- | --- |
| `Image Generator.ipynb` | Main notebook for installing dependencies, loading Stable Diffusion, and generating images. |
| `.gitignore` | Ignores local project files. |

## Features

- Text-to-image generation
- Stable Diffusion 2.1 model
- Google Colab friendly setup
- GPU acceleration with CUDA
- Custom prompt, width, and height settings
- Image preview with Matplotlib

## Recommended Environment

The easiest way to run this project is with Google Colab.

Requirements:

- Google Colab account
- GPU runtime enabled
- Internet connection for downloading model weights

You can also run it locally if your system has:

- Python 3.8 or newer
- NVIDIA GPU with CUDA support
- Enough VRAM for Stable Diffusion inference

## Running in Google Colab

1. Open Google Colab.
2. Upload or open `Image Generator.ipynb`.
3. Go to `Runtime` > `Change runtime type`.
4. Select `GPU`.
5. Run the notebook cells from top to bottom.

The notebook installs the required libraries:

```python
!pip install --upgrade diffusers transformers accelerate torch bitsandbytes scipy safetensors xformers --quiet
```

## How It Works

The notebook loads Stable Diffusion 2.1:

```python
model_id = "stabilityai/stable-diffusion-2-1"

pipe = StableDiffusionPipeline.from_pretrained(model_id, torch_dtype=torch.float16)
pipe.scheduler = DPMSolverMultistepScheduler.from_config(pipe.scheduler.config)
pipe = pipe.to("cuda")
```

Then it generates an image from a text prompt:

```python
prompt = "A nice looking image of a computer setup"
image = pipe(prompt, width=1000, height=1000).images[0]
```

The generated image is displayed with Matplotlib:

```python
plt.imshow(image)
plt.axis('off')
plt.show()
```

## Customizing the Prompt

Change the `prompt` value in the notebook to generate a different image.

Example:

```python
prompt = "A futuristic city skyline at sunset, cinematic lighting, ultra detailed"
```

You can also adjust the image size:

```python
image = pipe(prompt, width=768, height=768).images[0]
```

Large image sizes require more GPU memory. If Colab runs out of memory, reduce `width` and `height`.

## Running Locally

Clone the repository:

```bash
git clone https://github.com/Tech-Watt/Free-Image-Generator.git
cd Free-Image-Generator
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate it on Windows:

```bash
.venv\Scripts\activate
```

Activate it on macOS/Linux:

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install --upgrade diffusers transformers accelerate torch bitsandbytes scipy safetensors xformers matplotlib
```

Then open the notebook:

```bash
jupyter notebook "Image Generator.ipynb"
```

## Notes

- GPU runtime is strongly recommended.
- The first run may take time because the model weights need to download.
- Higher resolutions use more VRAM.
- If you are using Colab, restart the runtime if GPU memory becomes full.
- Generated images depend heavily on the prompt quality.

## Author

Created by [Tech Watt](https://github.com/Tech-Watt).
