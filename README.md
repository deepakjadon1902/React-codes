App.tsx :-
import "./App.css";
import { BrowserRouter, Route, Routes } from "react-router-dom";
import LoginForm from "./login";
import Table from "./table";
import HomePage  from "./home";
import Counter from "./counter";

const App = () => {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/home" element={<HomePage />} />
        <Route path="/login" element={<LoginForm />} />
        <Route path="/counter" element={<Counter />} />
        <Route path="/table" element={<Table />} />
      </Routes>
    </BrowserRouter>
  );
};

export default App;

home.tsx:-
import React, { useState } from 'react';
import './App.css';

const HomePage = () => {
  const [data, setData] = useState([]);

  return (
    <div className="home-page">
      <h1>Welcome to My Home Page</h1>
      <p>This is a sample home page.</p>
    </div>
  );
};

export default HomePage;

table.tsx:-
import { useState } from "react";
 import "./App.css"

 export const Table = () => {
const [data, setData] = useState([]);

   const getData = async () => {
     const response = await fetch("https://jsonplaceholder.typicode.com/users/");
     const responseValue = await response.json();
     console.log(responseValue);
     setData(responseValue);
   };

   const handleRemove = (index: number) => {
     setData(data.filter((_, i) => i !== index));
   };

   return (
     <>
       <button onClick={() => getData()}>Get Data</button>
       <button onClick={() => setData([])}>Reset</button>

       <table>
         <tr>
           <th>S.No</th>
           <th>Name</th>
           <th>User Name</th>
           <th>E-mail</th>
           <th>Phone</th>
           <th>Action</th>
         </tr>
         {data.map((user, index) => (
           <tr key={index}>
             <td>{index + 1}</td>
             <td>{user.name}</td>
             <td>{user.username}</td>
             <td>{user.email}</td>
             <td>{user.phone}</td>
             <td>
               <button onClick={() => handleRemove(index)}>Remove</button>
             </td>
           </tr>
         ))}
       </table>
     </>
);
 };

 export default Table;


 login.tsx:-
 import { useState } from "react";
import './App.css'
export const LoginForm = () => {
  const [data, setData] = useState({ email: "Initial", password: "Initial" });

  return (
    <><form>

      <label htmlFor="mail" className="mail"><b>Email: </b></label>
      <input className="mail" type="email" id="mail" name="mail" placeholder="Enter your mail" required onChange={(event) => setData({ ...data, email: event.target.value })} />
      <br />
      <br />
      <label htmlFor="password"><b>Password: </b></label>
      <input type="password" id="password" name="password" required placeholder="Enter password" onChange={(event) => setData({ ...data, password: event.target.value })} />
      <br />
      <br />
      
      <button className="button" type="submit"><b>Submit</b></button>
    </form>
      <h2 ><b>The entered email is {data.email} </b></h2>
      <h2><b>and the password is {data.password}</b></h2>
    </>
  )
};
export default LoginForm;

counter.tsx:-
const Counter  = (props) => {
    console.log("Counter props:",props)
    
    
        const {buttonLabel, color, count, countButtonClick} = props;
      
        return (
            <>
            <h3> This Button is clicked {count} times</h3>
            <button onClick={() => countButtonClick()}style ={{borderColor: color}}>
                 {buttonLabel} 
                 </button>
            
            </>
        );
     };
    export default Counter;


    App.css:-
    :root {
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;

  color-scheme: light dark;
  color: rgba(255, 255, 255, 0.87);
  background-color: #242424;

  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

a {
  font-weight: 500;
  color: #646cff;
  text-decoration: inherit;
}
a:hover {
  color: #535bf2;
}

body {
  margin: 0;
  display: flex;
  place-items: center;
  min-width: 320px;
  min-height: 100vh;
}

h1 {
  font-size: 3.2em;
  line-height: 1.1;
}

button {
  border-radius: 8px;
  border: 1px solid transparent;
  padding: 0.6em 1.2em;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  background-color: #1a1a1a;
  cursor: pointer;
  transition: border-color 0.25s;
}
button:hover {
  border-color: #646cff;
}
button:focus,
button:focus-visible {
  outline: 4px auto -webkit-focus-ring-color;
}

@media (prefers-color-scheme: light) {
  :root {
    color: #213547;
    background-color: #ffffff;
  }
  a:hover {
    color: #747bff;
  }
  button {
    background-color: #f9f9f9;
  }
}


  
