# Create AI for Generate Image

## Python Generate Image

* Check GPU runtime
```
$ !nvidia-smi
```

## Install the necessary libraries

```python
$ !pip install diffusers==0.11.1
$ !pip install transformers scipy ftfy accelerate
```

* Code

```python
import torch
from diffusers import StableDiffusionPipeline

pipe = StableDiffusionPipeline.from_pretrained("CompVis/stable-diffusion-v1-4"
, torch_dtype=torch.float16)
pipe = pipe.to("cuda")
prompt = "cat flying in space"

image = pipe(prompt,num_inference_steps=100).images[0]
image.save(f"image.png")
image
```

---
