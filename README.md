# AI Video & Image Generator Client

A lightweight, standalone Python SDK and CLI tool for orchestrating multi-model generative video and image synthesis workflows.

## Features
- **Video Generation:** Supports leading models (Kling, Runway, Luma, Google Veo) in Text-to-Video and Image-to-Video modes.
- **Image Generation:** Supports high-fidelity image models (FLUX 1.1, GPT-Image, Imagen).
- **Aspect Ratios:** Native support for widescreen (16:9), vertical reels/shorts (9:16), and square (1:1).
- **Keyframing & References:** Upload first-frame, last-frame, or style reference images.
- **Zero Dependencies:** Built entirely with Python's standard library (`urllib`, `json`, `argparse`).
- **Privacy & Security:** Tokens are dynamically resolved from environment variables or local paths, preventing secret leakage.

## Installation
Clone the repository:
```bash
git clone https://github.com/dalroot/ai-video-generator.git
cd ai-video-generator
```

No external pip packages are required.

## Configuration
Set your authentication token via environment variable:
```bash
export ADOBE_TOKEN="your_access_token_here"
```
Or place it in a `.token` file in the project root.

## CLI Usage

### Check Quota & Entitlements
```bash
python3 firefly_client.py check-auth --feature firefly_3p:external:kling_v3_ti2v
```

### Generate Video (Text-to-Video)
```bash
python3 firefly_client.py video \
  --model kling-3 \
  --prompt "Futuristic glowing neon geometric shapes morphing in zero gravity" \
  --aspect portrait \
  --duration 5 \
  --poll \
  --output reels_output.mp4
```

### Generate Video (Image-to-Video)
```bash
python3 firefly_client.py video \
  --model kling-3 \
  --prompt "Smooth camera pan around the character" \
  --first-frame start.png \
  --aspect portrait \
  --poll \
  --output output.mp4
```

### Generate Image
```bash
python3 firefly_client.py image \
  --model flux-pro-1.1 \
  --prompt "Studio macro shot of a diamond mechanical watch" \
  --poll \
  --output image.png
```

## Python API Usage

```python
from firefly_client import FireflyClient

client = FireflyClient()

# Generate video
job = client.generate_video(
    model_key="kling-3",
    prompt="Ocean waves glowing under moonlight",
    aspect_ratio="portrait",
    duration=5
)
print("Job created:", job)
```

## License
MIT License
