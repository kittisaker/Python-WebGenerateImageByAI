# Create AI for Generate Image

## FastAPI

* Installation
```
$ !pip install fastapi nest-asyncio pyngrok uvicorn

!ngrok config add-authtoken 2Vktl5xYJINv18FesZykb8pnwQK_6Hm9qtKwiQdmSZSxkQyJq
```

* Code

```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware
import nest_asyncio
from pyngrok import ngrok
import uvicorn

app = FastAPI()

app.add_middleware(
  CORSMiddleware,
  allow_origins=['*'],
  allow_credentials=True,
  allow_methods=['*'],
  allow_headers=['*'],
)

@app.get('/')
async def root():
  return {'hello' : 'world'}

ngrok_tunnel = ngrok.connect(8000)
print('Public URL:', ngrok_tunnel.public_url)

nest_asyncio.apply()
uvicorn.run(app, port=8000)
```

## Test More

```python
@app.get('/generate-image')
async def generate_image(prompt:str):
    image = pipe(prompt,num_inference_steps=100).images[0]
    buffer = BytesIO()
    image.save(buffer, format="PNG")
    imgstr = base64.b64encode(buffer.getvalue())
    return Response(content=imgstr, media_type="image/png")
```

```
!pip install fastapi nest-asyncio pyngrok uvicorn
!pip install diffusers==0.11.1
!pip install transformers scipy ftfy accelerate
!ngrok config add-authtoken 2Vktl5xYJINv18FesZykb8pnwQK_6Hm9qtKwiQdmSZSxkQyJq
```

* Code

```Python
import torch
from diffusers import StableDiffusionPipeline

from fastapi import FastAPI, Response
from fastapi.middleware.cors import CORSMiddleware

import nest_asyncio
from pyngrok import ngrok
import uvicorn
from io import BytesIO
import base64

pipe = StableDiffusionPipeline.from_pretrained("CompVis/stable-diffusion-v1-4", torch_dtype=torch.float16)
pipe = pipe.to("cuda")

app = FastAPI()

app.add_middleware(
  CORSMiddleware,
  allow_origins=['*'],
  allow_credentials=True,
  allow_methods=['*'],
  allow_headers=['*'],
)

@app.get('/')
async def root():
  return {'hello' : 'world'}

@app.get('/kope')
async def getName():
  return {'My name is kope'}

@app.get('/generate-image')
async def generate_image(prompt:str):
  image = pipe(prompt,num_inference_steps=100).images[0]
  buffer = BytesIO()
  image.save(f"image.png")
  image.save(buffer, format="PNG")
  imgstr = base64.b64encode(buffer.getvalue())
  return Response(content=imgstr, media_type="image/png")

ngrok_tunnel = ngrok.connect(8000)
print('Public URL:', ngrok_tunnel.public_url)

nest_asyncio.apply()
uvicorn.run(app, port=8000)
```

---