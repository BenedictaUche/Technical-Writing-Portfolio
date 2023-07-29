---
title: "How to implement a search bar functionality using the useState hook"
datePublished: Sun Jul 02 2023 19:17:34 GMT+0000 (Coordinated Universal Time)
cuid: cljltdu2g000109jh2mqobzoe
slug: how-to-implement-a-search-bar-functionality-using-the-usestate-hook
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/ayjnmG4oUX4/upload/f88f9a4db92855327bd56ce06fb6061f.jpeg
tags: reactjs, react-hooks, usestate, reacthooks, useeffect

---

## Introduction

This tutorial demonstrates how to create a search bar functionality using the useState hook in React. The useState hook empowers us to build a dynamic search bar that enables users to input search queries, instantly update search results, and improve the user experience. We will cover the necessary steps, including handling user input, filtering data, and updating the component state. Follow along to learn how to seamlessly integrate a search bar into your React application.

## Prerequisites

To get the most out of this tutorial, you should have a basic understanding of the following concepts and have the following tools:

* Familiarity with Javascript concepts like variables, functions, arrays, and objects
    
* Prior knowledge of React concepts like JSX syntax
    
* Familiarity with functional components in React
    
* Basic understanding of useState hook (optional)
    
* [Nodejs](https://nodejs.org/en/download) and npm
    
* [VSCode](https://code.visualstudio.com/download) or any preferred code editor
    

### What is the useState hook?

The **useState** hook is a built-in React hook that allows you to store and update data in a way that enables your components to react to changes in the data and update the UI accordingly.

With useState, a piece of information can be saved, like the colour of a ball, and change it whenever you want. This piece of information is called the **state**.

### STEP 1

1. In your terminal, create a [create-vite](https://www.jetbrains.com/help/webstorm/vite.html#create_new_vite_app) application and follow the steps after
    
    ```bash
    npx create-vite search #search is the name of our project
    ```
    
2. Select React as the framework and Javascript as the variant
    
3. cd into the search folder, install dependencies and open the folder in vscode
    
    ```bash
    cd search
    npm install
    code . #command to open vscode from terminal
    ```
    
4. Ctrl+j to open VSCode terminal and run this command to run the application locally
    
    ```bash
    npm run dev
    ```
    
5. After running the application, visit the [http://localhost:5173/](http://localhost:5173/) in your web browser to verify that the application is running
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688303993273/8ab86988-476f-411a-8651-40eeff890892.png align="center")
    

*You should see this on the browser*

### STEP 2

1. Create a `components` folder and create a `Catalog.jsx` file in the folder
    
    ```bash
    .
    ├── node_modules   
    ├── public
    ├── src
    │   ├── assets       
    │   ├── components  
    │         ├── Catalog.jsx   
    │   ├── App.css
    │   ├── App.jsx 
    │   ├── index.css
    │   └── main.jsx 
    ├── .eslintrc.cjs     
    ├── .gitignore
    ├── index.html     
    ├── package-lock.json       
    ├── package.json     
    └── vite.config.js
    ```
    

*Your file structure should look like this*

1. Type `rfc + Tab` to get the skeleton for the Catalog.jsx file or copy and paste the code:
    
    ```bash
    export default function Catalog() {
      return (
        <div>Catalog</div>
      )
    }
    ```
    
2. Clear out your `App.jsx` file as it will not be needed. Import the Catalog into the App.jsx. It should look so
    
    ```bash
    import Catalog from "./components/Catalog"
    
    function App() {
      return (
        <>
          <Catalog />
        </>
      )
    }
    
    export default App
    ```
    

### STEP 3

1. Create a list of items in the `Catalog.jsx` file
    
    ```bash
    export default function Catalog() {
    
        const items = [
            {
                id: 1,
                name: 'Xena',
                description: 'Happy Dog',
                image: 'https://media.istockphoto.com/id/1328887289/photo/happy-dog.jpg?b=1&s=170667a&w=0&k=20&c=mp3L73BC14QUuk1EQaYtZ1-wwJRW9HAffcsGZNyMy_o=',
            },
            {
                id: 2,
                name: 'Leo and Catty',
                description: 'Labrador retriever and a ginger cat',
                image: 'https://media.istockphoto.com/id/1435010849/photo/labrador-retriever-dog-panting-and-ginger-cat-sitting-in-front-of-dark-yellow-background.jpg?b=1&s=170667a&w=0&k=20&c=Rr2nJh68FjKPZKvB6VPwnCHT4QEOZR9g_Xh7OxbMIcc=',
            },
            {
                id: 3,
                name: 'Shorty',
                description: 'Dog looking out from car window',
                image: 'https://media.istockphoto.com/id/1387718984/photo/dachshund-dog-riding-in-car-and-looking-out-from-car-window-happy-dog-enjoying-life-dog.jpg?b=1&s=170667a&w=0&k=20&c=JKPWeo0O5HC0kQTHC3Ux_PEG3K64oT-AcLg6TP5pMFQ=',
            },
        ];
        
      return (
        <div>Catalog</div>
      )
    }
    ```
    
2. Create and style input component
    
    ```bash
    
    export default function Catalog() {
    
        const items = [
            {
                id: 1,
                name: 'Xena',
                description: 'Happy Dog',
                image: 'https://media.istockphoto.com/id/1328887289/photo/happy-dog.jpg?b=1&s=170667a&w=0&k=20&c=mp3L73BC14QUuk1EQaYtZ1-wwJRW9HAffcsGZNyMy_o=',
            },
            {
                id: 2,
                name: 'Leo and Catty',
                description: 'Labrador retriever and a ginger cat',
                image: 'https://media.istockphoto.com/id/1435010849/photo/labrador-retriever-dog-panting-and-ginger-cat-sitting-in-front-of-dark-yellow-background.jpg?b=1&s=170667a&w=0&k=20&c=Rr2nJh68FjKPZKvB6VPwnCHT4QEOZR9g_Xh7OxbMIcc=',
            },
            {
                id: 3,
                name: 'Shorty',
                description: 'Dog looking out from car window',
                image: 'https://media.istockphoto.com/id/1387718984/photo/dachshund-dog-riding-in-car-and-looking-out-from-car-window-happy-dog-enjoying-life-dog.jpg?b=1&s=170667a&w=0&k=20&c=JKPWeo0O5HC0kQTHC3Ux_PEG3K64oT-AcLg6TP5pMFQ=',
            },
        ];
        
      return (
        <div>
           <input type="text" class="" placeholder="Enter text..."
                    style={{ width: '40vw', height: '5vh', borderRadius: '8px', 
                             border: 'none', outlineColor: 'lightcoral'style={{textAlign: 'center',}} 
                           }}
            />
        </div>
      )
    }
    ```
    
3. Map through the items array to get information like so
    
    ```bash
    
    export default function Catalog() {
    
        const items = [
            {
                id: 1,
                name: 'Xena',
                description: 'Happy Dog',
                image: 'https://media.istockphoto.com/id/1328887289/photo/happy-dog.jpg?b=1&s=170667a&w=0&k=20&c=mp3L73BC14QUuk1EQaYtZ1-wwJRW9HAffcsGZNyMy_o=',
            },
            {
                id: 2,
                name: 'Leo and Catty',
                description: 'Labrador retriever and a ginger cat',
                image: 'https://media.istockphoto.com/id/1435010849/photo/labrador-retriever-dog-panting-and-ginger-cat-sitting-in-front-of-dark-yellow-background.jpg?b=1&s=170667a&w=0&k=20&c=Rr2nJh68FjKPZKvB6VPwnCHT4QEOZR9g_Xh7OxbMIcc=',
            },
            {
                id: 3,
                name: 'Shorty',
                description: 'Dog looking out from car window',
                image: 'https://media.istockphoto.com/id/1387718984/photo/dachshund-dog-riding-in-car-and-looking-out-from-car-window-happy-dog-enjoying-life-dog.jpg?b=1&s=170667a&w=0&k=20&c=JKPWeo0O5HC0kQTHC3Ux_PEG3K64oT-AcLg6TP5pMFQ=',
            },
        ];
    
      return (
        <div>
            <input type="text" class="" placeholder="Enter text..."
                style={{ width: '40vw', height: '5vh', borderRadius: '8px', border: 'none', outlineColor: 'lightcoral', display: 'block', margin: '0 auto' }}
            />
            <div style={{ display: 'flex' }}>
                {items.map((item) => (
                    <div key={item.id}>
                        <img src={item.image} alt={item.name} style={{ maxWidth: '80%', height: 'auto', margin: '5%' }} />
                        <h3 style={{textAlign: 'center',}}>{item.name}</h3>
                        <p style={{textAlign: 'center',}}>{item.description}</p>
                    </div>
                ))}
            </div>
        </div>
      )
    }
    ```
    
4. At the very top of the `Catalog.jsx` file, import `useState` from react
    
    ```bash
    import {useState} from 'react'
    
    #....Rest of the code
    ```
    

### STEP 4

1. Still in the `Catalog.jsx` file, create ***searchTerm*** and ***searchResult*** states to keep track of what we type into the search bar and keep track of all the data that match what we typed into the search bar respectively
    
    ```bash
    import {useState} from 'react'
    
    export default function Catalog() {
    
        const [searchTerm, setSearchTerm] = useState('');
        const [searchResults, setSearchResults] = useState([]);
    
        #..items array
    
      return (
        <div>
            #..remaining code
        </div>
      )
    }
    ```
    
2. Create a `handleChange` function to handle changes in the input field
    
    ```bash
    import {useState} from 'react'
    
    export default function Catalog() {
    
        const [searchTerm, setSearchTerm] = useState('');
        const [searchResults, setSearchResults] = useState([]);
    
        const handleChange = event => {
            setSearchTerm(event.target.value);
        };
    
        #....items array
    
      return (
        <div>
            #..remaining code
        </div>
      )
    }
    ```
    
3. To the input field add the `handleChange` function to handle changes
    
4. Add the `searchTerm` to the input value so that when the `handleChange` is triggered, it updates the `searchTerm` state variable with the current value of the input.
    
    ```bash
    import {useState} from 'react'
    
    export default function Catalog() {
    
        const [searchTerm, setSearchTerm] = useState('');
        const [searchResults, setSearchResults] = useState([]);
    
        const handleChange = event => {
            setSearchTerm(event.target.value);
        };
    
        #...items array
    
      return (
        <div>
            <input type="text" class="" placeholder="Enter text..."
            onChange={handleChange}
            value={searchTerm}
                style={{ width: '40vw', height: '5vh', borderRadius: '8px', border: 'none', outlineColor: 'lightcoral', display: 'block', margin: '0 auto' }}
            />
            <div style={{ display: 'flex' }}>
                {items.map((item) => (
                    <div key={item.id}>
    
                        <img src={item.image} alt={item.name} style={{ maxWidth: '80%', height: 'auto', margin: '5%' }} />
                        <h3 style={{textAlign: 'center',}}>{item.name}</h3>
                        <p style={{textAlign: 'center',}}>{item.description}</p>
                    </div>
                ))}
            </div>
        </div>
      )
    }
    ```
    

### STEP 5

1. Import `useEffect` at the top of the `Catalog.jsx` file
    
    ```bash
    import {useState, useEffect} from 'react'
    
    #....Rest of the code
    ```
    
2. Define a `useEffect` hook that takes two arguments: a callback function and a dependency array.
    
    ```bash
    useEffect(() => {callback}, [dependency_array]);
    ```
    
3. Inside the `callback` function, filter the `items` array using the `filter` method.
    
4. For each item, check if its lowercase `name` property includes the lowercase `searchTerm` value. This check is case-insensitive, as both the `name` and `searchTerm` are converted to lowercase using the `toLowerCase()` method.
    
5. Store the filtered results in a variable called `results`.
    
    ```bash
    import {useState, useEffect} from 'react'
    
    export default function Catalog() {
    
        const [searchTerm, setSearchTerm] = useState('');
        const [searchResults, setSearchResults] = useState([]);
    
        const handleChange = event => {
            setSearchTerm(event.target.value);
        };
    
        useEffect(() => {
            const results = items.filter(item =>
                item.name.toLowerCase().includes(searchTerm.toLowerCase())
            );
        }, []);
    
        #..items array
    
      return (
        <div>
            <input type="text" class="" placeholder="Enter text..."
            onChange={handleChange}
            value={searchTerm}
                style={{ width: '40vw', height: '5vh', borderRadius: '8px', border: 'none', outlineColor: 'lightcoral', display: 'block', margin: '0 auto' }}
            />
            <div style={{ display: 'flex' }}>
                {items.map((item) => (
                    <div key={item.id}>
    
                        <img src={item.image} alt={item.name} style={{ maxWidth: '80%', height: 'auto', margin: '5%' }} />
                        <h3 style={{textAlign: 'center',}}>{item.name}</h3>
                        <p style={{textAlign: 'center',}}>{item.description}</p>
                    </div>
                ))}
            </div>
        </div>
      )
    }
    ```
    
6. Call the `setSearchResults` function, obtained from the `useState` hook, with the `results` variable as the argument. This updates the `searchResults` state variable with the filtered results.
    
    ```bash
    import {useState, useEffect} from 'react'
    
    export default function Catalog() {
    
        const [searchTerm, setSearchTerm] = useState('');
        const [searchResults, setSearchResults] = useState([]);
    
        const handleChange = event => {
            setSearchTerm(event.target.value);
        };
    
        useEffect(() => {
            const results = items.filter(item =>
                item.name.toLowerCase().includes(searchTerm.toLowerCase())
            );
            setSearchResults(results);
        }, []);
    
        #...items array
    
      return (
        <div>
            <input type="text" class="" placeholder="Enter text..."
            onChange={handleChange}
            value={searchTerm}
                style={{ width: '40vw', height: '5vh', borderRadius: '8px', border: 'none', outlineColor: 'lightcoral', display: 'block', margin: '0 auto' }}
            />
            <div style={{ display: 'flex' }}>
                {items.map((item) => (
                    <div key={item.id}>
    
                        <img src={item.image} alt={item.name} style={{ maxWidth: '80%', height: 'auto', margin: '5%' }} />
                        <h3 style={{textAlign: 'center',}}>{item.name}</h3>
                        <p style={{textAlign: 'center',}}>{item.description}</p>
                    </div>
                ))}
            </div>
        </div>
      )
    }
    ```
    
7. In the second argument, dependency array, put the `searchTerm`. Whenever the value of `searchTerm` changes, the callback function inside the `useEffect` hook will be executed again.
    
    ```bash
    import {useState, useEffect} from 'react'
    
    export default function Catalog() {
    
        const [searchTerm, setSearchTerm] = useState('');
        const [searchResults, setSearchResults] = useState([]);
    
        const handleChange = event => {
            setSearchTerm(event.target.value);
        };
    
        useEffect(() => {
            const results = items.filter(item =>
                item.name.toLowerCase().includes(searchTerm.toLowerCase())
            );
            setSearchResults(results);
        }, [searchTerm]);
    
        #...items array
    
      return (
        <div>
            <input type="text" class="" placeholder="Enter text..."
            onChange={handleChange}
            value={searchTerm}
                style={{ width: '40vw', height: '5vh', borderRadius: '8px', border: 'none', outlineColor: 'lightcoral', display: 'block', margin: '0 auto' }}
            />
            <div style={{ display: 'flex' }}>
                {items.map((item) => (
                    <div key={item.id}>
    
                        <img src={item.image} alt={item.name} style={{ maxWidth: '80%', height: 'auto', margin: '5%' }} />
                        <h3 style={{textAlign: 'center',}}>{item.name}</h3>
                        <p style={{textAlign: 'center',}}>{item.description}</p>
                    </div>
                ))}
            </div>
        </div>
      )
    }
    ```
    
8. Replace `items.map` with `searchResults.map`
    
    ```bash
    import {useState, useEffect} from 'react'
    
    export default function Catalog() {
    
        const [searchTerm, setSearchTerm] = useState('');
        const [searchResults, setSearchResults] = useState([]);
    
        const handleChange = event => {
            setSearchTerm(event.target.value);
        };
    
        useEffect(() => {
            const results = items.filter(item =>
                item.name.toLowerCase().includes(searchTerm.toLowerCase())
            );
            setSearchResults(results);
        }, [searchTerm]);
    
        const items = [
            {
                id: 1,
                name: 'Xena',
                description: 'Happy Dog',
                image: 'https://media.istockphoto.com/id/1328887289/photo/happy-dog.jpg?b=1&s=170667a&w=0&k=20&c=mp3L73BC14QUuk1EQaYtZ1-wwJRW9HAffcsGZNyMy_o=',
            },
            {
                id: 2,
                name: 'Leo and Catty',
                description: 'Labrador retriever and a ginger cat',
                image: 'https://media.istockphoto.com/id/1435010849/photo/labrador-retriever-dog-panting-and-ginger-cat-sitting-in-front-of-dark-yellow-background.jpg?b=1&s=170667a&w=0&k=20&c=Rr2nJh68FjKPZKvB6VPwnCHT4QEOZR9g_Xh7OxbMIcc=',
            },
            {
                id: 3,
                name: 'Shorty',
                description: 'Dog looking out from car window',
                image: 'https://media.istockphoto.com/id/1387718984/photo/dachshund-dog-riding-in-car-and-looking-out-from-car-window-happy-dog-enjoying-life-dog.jpg?b=1&s=170667a&w=0&k=20&c=JKPWeo0O5HC0kQTHC3Ux_PEG3K64oT-AcLg6TP5pMFQ=',
            },
        ];
    
      return (
        <div>
            <input type="text" class="" placeholder="Enter text..."
                onChange={handleChange}
                value={searchTerm}
                style={{ width: '40vw', height: '5vh', borderRadius: '8px', border: 'none', outlineColor: 'lightcoral', display: 'block', margin: '0 auto' }}
            />
            <div style={{ display: 'flex' }}>
                {searchResults.map((item) => (
                    <div key={item.id}>
    
                        <img src={item.image} alt={item.name} style={{ maxWidth: '80%', height: 'auto', margin: '5%' }} />
                        <h3 style={{textAlign: 'center',}}>{item.name}</h3>
                        <p style={{textAlign: 'center',}}>{item.description}</p>
                    </div>
                ))}
            </div>
        </div>
      )
    }
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688319594464/d3a7fa8e-e21d-44cd-b038-b9e9a659230c.gif align="center")

## CONCLUSION

You have successfully implemented a search bar functionality using the useState and useEffect hooks in React. By leveraging these powerful hooks, you have enabled dynamic searching based on user input and updated the search results accordingly. This example showcases the simplicity and effectiveness of React hooks in managing state and side effects.

Now that you have implemented a search bar functionality with the useState and useEffect hooks consider exploring other React hooks to enhance your website functionality.

## ADDITIONAL CONSIDERATIONS AND BEST PRACTICES

* Always remember to save your code! Regularly saving your work ensures that you don't lose any important changes or progress made during the development process.
    
* If the search bar and search results are used across multiple components or pages, consider extracting them into reusable components for better code organization and reusability.
    

## RESOURCES

* [React official documentation](https://react.dev/blog/2023/03/16/introducing-react-dev)
    
* [Vite documentation](https://www.jetbrains.com/help/webstorm/vite.html)