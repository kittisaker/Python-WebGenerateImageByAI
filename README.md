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

```java
@app.get('/generate-image')
async def generate_image(prompt:str):
    image = pipe(prompt,num_inference_steps=100).images[0]
    buffer = BytesIO()
    image.save(buffer, format="PNG")
    imgstr = base64.b64encode(buffer.getvalue())
    return Response(content=imgstr, media_type="image/png")
```

---