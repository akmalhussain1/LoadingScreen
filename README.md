
# LoadingScreen.jsx

import React, { useEffect, useState } from 'react'

const LoadingScreen = ({onComplete}) => {

const[text,setText]=useState("");

const fullText="<Hello World/>";

useEffect(()=>{
  let index= 0;
  const interval =setInterval(()=>{
    setText(fullText.substring(0, index));
    index++;

    if(index > fullText.length){
      clearInterval(interval);

      setTimeout(()=>{
        onComplete();
      },1000);
    }
}, 100 );
return()=>clearInterval(interval);
},[onComplete]);

  return (
    <>
      <div className="fixed inset-0 z-50  bg-black text-gray-100 flex flex-col items-center justify-center">
     <div className="mb-4 text-4xl font-mono font-bold">{text} <span className="animate-blink ml-1"> |</span>
     </div>
      
      <div className="w-[200px] h-[2px] bg-gray-800 rounded relative overflow-hidden">
       <div className="w-[40%] h-full bg-blue-500 shadow-[0_0_15px_#3b82f6] animate-loading-bar">
        {""}
       </div>
      </div>
      </div>
    </>
  )
}

export default LoadingScreen


# Index.css 
@import "tailwindcss";
html,body{
  margin: 0;
  padding: 0;
  font-family: "Space Grotesk",sans-serif;
  background: #0a0a0a;
  color: #f3f4f6;
}
@layer utilities{
  @keyframes loading{
    0%{
  transform: translateX(-100%);
    }
    100%{
    transform: translateX(250%);
    }
  }
  .animate-loading-bar{
    animation: loading 0.8s ease infinite;
  }
}


# App.jsx
import React, { useState } from 'react'
import './index.css'
import LoadingScreen from './components/LoadingScreen'
const App = () => {
const [isLoaded, setIsLoaded] = useState(false)

    return (
    <>
    {!isLoaded && <LoadingScreen onComplete={()=>setIsLoaded(true)}/> }
    </>
  )
}

export default App


