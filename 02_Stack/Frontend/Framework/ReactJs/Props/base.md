# Props
```bash
- Là các đối số được truyền vào các thành phần React. Props được truyền vào các thành phần thông qua các thuộc tính HTML. Props là viết tắt của properties.
```
**Ex**
**src/App.jsx**
```js
function User(props){
  return <p>{props.name} - {props.age}</p>
}

export default function App() {
  return (
    <>
      <User name="Thắng" age={22}/>
    </>
  )
}
```
**src/main.jsx**
```js
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import App from './App.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>
)
```

