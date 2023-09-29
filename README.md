# Create AI for Generate Image

## Installation and Set enviroment

* Visual Studio Code
* NodeJS

```shell
$ node -v

$ npm -v
```

### Create React project

```shell
$ npx create-react-app my-app
```

Run project
```shell
$ cd web-ai-image
$ npm run start
```

### Install Tailwind CSS :[tailwindcss](https://tailwindcss.com/docs/guides/create-react-app)

```shell
$ npm install -D tailwindcss
$ npx tailwindcss init
```

#### Configure your template paths

<details>
<summary>tailwind.config.js</summary>

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./src/**/*.{js,jsx,ts,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

</details>

#### Add the Tailwind directives to your CSS

<details>
<summary>index.css</summary>

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

</details>
</br>
* Run project

```shell
$ npm run start
```

#### Start using Tailwind in your project : [Ref](https://tailwindcss.com/docs/text-color)

<details>
<summary>App.js</summary>

```js
export default function App() {
  return (
    <h1 className="text-3xl font-bold underline">
      Hello world!
    </h1>
  )
}
```

</details>

### Installation Axios : [Ref](https://axios-http.com/docs/intro)

```shell
$ npm install axios
```

### About UX/UI

- [figma](https://www.figma.com/file/EdB9rCr3JSk6DWU6pJAvv3/Flowbite-Design-System-(Community)?type=design&node-id=1002-2&mode=design&t=TH78suB7mKzv09Bo-0)
- [Flowbite](https://flowbite.com/)

<details>
<summary>App.js</summary>

```js
import { useState } from 'react';
import './App.css';

function App() {

  const [keyword, setKeyword] = useState('kope')

  const handleInput = (e) => {
    // console.log('event', e.target.value)
    setKeyword(e.target.value)
  }
  
  return (
    <div className='bg-[#F5F5F5] h-[100vh] flex flex-col items-center'>
      <div className='max-w-[834px] w-full space-y-4'>
        <h2 className='text-[28px] font-[600]'>Welcom to KopeGPT : Generate Image with AI</h2>
        
        <form>   
            <label for="default-search" class="mb-2 text-sm font-medium text-gray-900 sr-only dark:text-white">Search</label>
            <div class="relative">
                <div class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none">
                    <svg class="w-4 h-4 text-gray-500 dark:text-gray-400" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20">
                        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z"/>
                    </svg>
                </div>
                <input onChange={handleInput} type="search" id="default-search" class="block w-full p-4 pl-10 text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Search Mockups, Logos..."></input>
                <button type="submit" class="text-white absolute right-2.5 bottom-2.5 bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-4 py-2 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Search</button>
            </div>
        </form>

        <div className='bg-white w-full h-[600px]'>
          {keyword}
        </div>

      </div>
    </div>
  );
}

export default App;
```

</details>

## Integration with api

<details>
<summary>App.js</summary>

```js
import { useState } from 'react';
import './App.css';
import axios from 'axios';

function App() {
  
  const [keyword, setKeyword] = useState('error')
  const [image, setImage] = useState('')

  const handleInput = (e) => {
    // console.log('event', e.target.value)
    setKeyword(e.target.value)
  }

  const callGenerateImage = async (e) => {
    e.preventDefault()
    const response = await axios.get(
      `https://fbc8-34-124-236-186.ngrok-free.app/generate-image?prompt=${keyword}`, {
      headers:{
        'ngrok-skip-browser-warning': true,
      }
    })
    // console.log('response', response)
    setImage('data:image/gif;base64, ' + response.data )
  }
  
  return (
    <div className='bg-[#F5F5F5] h-[100vh] flex flex-col items-center'>
      <div className='max-w-[834px] w-full space-y-4'>
        <h2 className='text-[28px] font-[600]'>Welcom to KopeGPT : Generate Image with AI</h2>
        
        <form onSubmit={callGenerateImage}>   
            <label for="default-search" class="mb-2 text-sm font-medium text-gray-900 sr-only dark:text-white">Search</label>
            <div class="relative">
                <div class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none">
                    <svg class="w-4 h-4 text-gray-500 dark:text-gray-400" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20">
                        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z"/>
                    </svg>
                </div>
                <input onChange={handleInput} type="search" id="default-search" class="block w-full p-4 pl-10 text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Search Mockups, Logos..."></input>
                <button type="submit" class="text-white absolute right-2.5 bottom-2.5 bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-4 py-2 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Search</button>
            </div>
        </form>

        <div className='bg-white w-full h-[600px]'>
          {image && <img src={image} alt='' />}
        </div>

      </div>
    </div>
  );
}

export default App;
```

</details>

## Build and Deploy

```shell
$ npm run build
```

* Deploy in cloudflare
  1. sign up for cloudflare
  2. Go to the manu <b>Workers & Pages</b>
  3. Click the button <b>Create Application</b>
  4. Go to tab <b>Pages</b>
  5. At title <b>Create using direct upload</b> click button <b>Upload assets</b>
  6. Create name and Upload folder name <b>build</b>

</details>

## About git

```shell
$ npm install

$ npm run start
```

---