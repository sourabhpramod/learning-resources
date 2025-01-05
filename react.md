# Basics of React.js

### To start:

```bash
npx create-react-app my-app
```
To start the react app server:

```bash
cd my-app
npm start
```

### To create a simple react component:
Inside the src folder 
create the needed file : welcome.js (or something)

inside welcome.js
```js
import React from 'react';

function Welcome(props){
    return <h1>Hello, {props.name}!</h1>;  //kinda returns an html page (jsx element)
}

export default Welcome;
```

### To use the component we created above:
Delete everything in app.js
and add:
```js
import React from 'react';
import Welcome from './welcome';

function App(){
  return (
    <div>
      <Welcome name="Alice"/>  //this is how we access components
      <Welcome name="Bob"/>
      <Welcome name="Charlie"/>
    </div>
  );
}

export default App;
```

### Using states in react for changes:
```js
import { useState } from 'react';
import './App.css';



const App = ()=> {
  const[counter, setCounter] = useState(0);

  const name = 'john'
  return (
    <div className="App">
      <button onClick={()=>{
        setCounter((prevCount)=>prevCount+1)
      }}>+</button>
      <h1>{counter}</h1>
      <button onClick={()=>{
        setCounter((prevCount)=>prevCount-1)
      }}>-</button>

    </div>
  );
}

export default App;

```
### State and life-cycle methods:

The below example uses both state and lifecycle methods

```js

import React, { Component } from 'react';


class Clock extends Component{
    constructor(props){
        super(props);
        this.state = {date: new Date()};
    }

    componentDidMount(){
        this.timerID = setInterval(()=>this.tick(), 1000);

    }

    componentWillUnmount(){
        clearInterval(this.timerID);
    }

    tick(){
        this.setState({
            date: new Date()
        });
    }

    render(){
        return (
            <div>
                <h1>
                    Hello, World!
                </h1>
                <h2>It is {this.state.date.toLocaleDateString()}.</h2>
            </div>
        );
    }
}
```

# HOOKS, CONTEXT AND PERFORMANCE APPLICATION
## Learn advanced
