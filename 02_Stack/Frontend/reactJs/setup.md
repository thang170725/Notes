- [React hoạt động như thế nào?](#react-hoạt-động-như-thế-nào)
- [Cách cài đặt ReactJS trên Linux](#cách-cài-đặt-reactjs-trên-linux)
- [Kiểm tra react đã được thêm vào dự án hay chưa](#kiểm-tra-react-đã-được-thêm-vào-dự-án-hay-chưa)
- [Upgrade to React 18](#upgrade-to-react-18)
- [Cấu trúc test \& luồng hoạt động](#cấu-trúc-test--luồng-hoạt-động)

---

- ReactJS là một fameswork bổ trợ thiết lập giao diện người dùng. Rất hot trong lập trình web.
    • Cộng đồng lớn
    • Được đánh giá thân thiện với SEO
    • Khả năng mở rộng tốt, tái sử dụng cao
    • Hiệu suất cao
    • Phát triển nhanh chóng
    • Khả năng tương thích ngược
    • Tương lai sáng
- ReactJS được sử dụng để xây dụng ứng dụng 1 trang.
- React cho phép chúng ta tạo các thành phần UI có thể tái sử dụng.
- React là một khuôn khổ Javascript frontend, là một thư viên Javascript do FaceBook tạo ra.

# React hoạt động như thế nào?
Thay vì thao tác trức tiếp DOM của trình duyệt, React tạo ra một DOM ảo trong bộ nhớ, nơi nó thực hiện tất cả các thao tác cần thiết, trước khi thức hiện các thay đổi trong DOM của trình duyệt.

# Cách cài đặt ReactJS trên Linux
    1. sudo apt update
    2. sudo apt install curl -y
    3. curl --version
    4. curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
    5. source ~/.bashrc   # hoặc ~/.zshrc nếu dùng zsh
    6. nvm install --lts
    7. nvm use --lts
    8. npx create-react-app my-app
    9. cd my-app
    10. npm start

# Kiểm tra react đã được thêm vào dự án hay chưa
1. npx create-react-app my-app. my-app là tên dự án
2. cd my-app. 
3. npm list react – Kiểm tra version của dự án react. Nếu chưa có. Chạy lệnh npm install react react-dom.
4. npm start. ReactJs sẽ chạy dự án mặc định ở port 3000, ta có thể mở trình duyệt và truy cập đường dẫn http://localhost:3000.

# Upgrade to React 18
Để nâng cấp phiên bản của react lên phiên bản mới nhất.
Từ thư mục dự án gỡ lệnh: npm i react@latest react-dom@latest

# Cấu trúc test & luồng hoạt động
Xem trong link này để hiểu rõ cấu trúc: [form-frontend](../../microservice/form.md)
**Flow Chart**
```bash
1. khi gõ npm start: sẽ gọi đến script trong package.json
  "start": "react-scripts start"
  - bật dev server
  - đọc public/index.html
  - tìm entry JS

2. public/index.html: của ngõ duy nhất
  trình duyệt chỉ thấy một div trống, react sẽ nhét toàn bộ app vào đây.
  React không chạy từ src/ trực tiếp

3. src/index.js: entry point
  Lấy <div id="root"> Render App component vào đó
  File này KHÔNG nên chứa logic → chỉ là “công tắc bật app”

4. src/App.jsx: root component, Component cao nhất
  Quản lý: layout tổng, router, provider (sau này)

5. pages/HomePage.jsx: 'Mỗi trang = 1 file' (Đại diện cho 1 màn hình)
  Gọi:
  - components
  - services
  KHÔNG chứa:
  - logic phức tạp
  - gọi API trực tiếp (nhiều)
  Nếu app có router → pages là nơi map route

6. components/: Cục gạch UI
  Chức năng: Component nhỏ, Tái sử dụng
  Không biết:
  - API ở đâu
  - state toàn cục
components không import services

7. services/: giao tiếp với backend
  Chức năng:
  - Gọi API
  - Trả data “sạch”
  UI KHÔNG fetch trực tiếp. Đổi backend → sửa 1 chỗ.

8. styles/ – STYLE TOÀN CỤC / MODULE
  Chức năng: CSS, theme, layout chung
  Không nhét CSS lung tung vào component khi project lớn

9. utils/ – CÔNG CỤ HỖ TRỢ
  Ví dụ:
  utils/
  └── formatDate.js
  Hàm nhỏ. Không phụ thuộc React
  Dùng cho: components, services

10. constants/ – HẰNG SỐ HỆ THỐNG
  export const API_URL = "http://localhost:8080";
  Tránh hard-code

11. hooks/ (chưa dùng)
  Custom hook: useUser(), useAuth()
  Logic React tái sử dụng

12. store/ (chưa dùng)
  State global: Redux, Zustand, Context
  Khi state vượt quá 2–3 component
```
**index.js**
```js
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import "./styles/main.css";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<App />);
```
**src/App.jsx**
```jsx
import HomePage from "./pages/HomePage";

function App() {
  return (
    <div>
      <h1>CRA Architecture Test</h1>
      <HomePage />
    </div>
  );
}

export default App;
```
**src/pages/HomePage.jsx**
```jsx
import Hello from "../components/Hello";

export default function HomePage() {
  return (
    <div>
      <p>This is Home Page</p>
      <Hello name="React CRA" />
    </div>
  );
}
```
**src/components/Hello.jsx**
```jsx
export default function Hello({ name }) {
  return <h2>Hello {name} 👋</h2>;
}
```
**src/services/user.service.js**
```js
export function getUserMock() {
  return {
    id: 1,
    name: "Test User",
  };
}
```
**src/styles/main.css**
```css
body {
  font-family: sans-serif;
}
```
**Chạy app**
```bash
cd frontend/web-cra
npm start
```

Phần 2
React Render HTML
React hiển thị HTML cho trang web bằng cách sử dụng hàm có tên là createRoot() và phương thức render.
createRoot()
Để lấy một đối số, một phần tử HTML.
Mục đích của hàm là xác định phần tử HTML nơi thành phần React sẽ được hiển thị.
render()
Được gọi để xác định thành phần React sẽ được hiển thị.
Hiển thị ở đâu?
Có một thư mục khác trong thư mục gốc của dự án React có tên là pubic trong thư mục này có một tệp là index.html
Bạn sẽ thấy một div duy nhất trong phần thân của tệp này. Đây là nơi ứng dụng React sẽ được hiển thị.

Cần vào thư mục dự án chạy lệnh npm start mới có thể mở trình duyệt.
import React from "react";
import ReactDOM from "react-dom/client";
const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(<div>hello world!!!</div>);

import React from 'react';
import ReactDOM from 'react-dom/client';

const myelement = (
  <table>
    <tr>
      <th>Name</th>
    </tr>
    <tr>
      <td>John</td>
    </tr>
    <tr>
      <td>Elsa</td>
    </tr>
  </table>
);

const container = document.getElementById('root');
const root = ReactDOM.createRoot(container);
root.render(myelement);
React JSX
JSX – Javascript XML
    • Cho phép viết các đoạn mã HTML trong React một cách dễ dàng và có cấu trúc hơn. React sử dụng JSX để xây dựng bố cục thay vì javascript thông thường. JSX giúp tạo ra các React element.
    • JSX giúp cho việc xây dựng các ứng dụng một cách nhanh hơn, dễ tối ưu trong việc biên soạn code sang js.
    • JSX dễ xem lỗi trong quá trình triển khai bởi hầu hết các lỗi sẽ được hiển thị trong quá trình biên soạn, không như các đoạn mã HTML có thể thừa thiếu các thẻ khiến trình biên dịch hiển thị sai. JSX thì hoàn toàn ngược lại nó sẽ hiển thị lỗi.
    • Cú pháp khá giống với HTML nên dễ dàng cho việc chuyển đổi.
Nếu code React trong file HTML. Phải lick thư viện Babel vào HTML. Tạo ra biến gắn tất cả thẻ giống như gán biến bằng thẻ. Tất cả các code js ở trong {}, {{}}, ‘’, “”. Phải lấy link JSX code mới chạy được và thêm type=”text/babel”.

import React from "react";
import ReactDOM from "react-dom/client";

let myElement = <h1 id="greet">Welcome to ReactJs</h1>;

const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(myElement);

import React from 'react';
import ReactDOM from 'react-dom/client';

const myElement = <h1>I Love JSX!</h1>;

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);

import React from 'react';
import ReactDOM from 'react-dom/client';

const myElement = <h1>React is {5 + 5} times better with JSX</h1>;

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);

import React from 'react';import ReactDOM from 'react-dom/client';

const myElement = (
  <ul>
    <li>Apples</li>
    <li>Bananas</li>
    <li>Cherries</li>
  </ul>);

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);

import React from 'react';import ReactDOM from 'react-dom/client';
const myElement = (
    <>
      <p>I am a paragraph.</p>
      <p>I am a paragraph too.</p>
    </>
  );
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);
<body>
  <div id="root">
    <p>I am a paragraph.</p>
    <p>I am a paragraph too.</p>
  </div>
</body>

React.createElement()
Để tạo ra đối tượng.
Cú pháp: React.createElement(value1, value2, value3);
    • Value1 là thẻ, function
    • Value2 là object
    • Value3 là nội dung
import React from 'react';
import ReactDOM from 'react-dom/client';

const myElement = React.createElement('h1', {}, 'I do not use JSX!');

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);
className
Để đặt tên class cho các thẻ HTML
import React from 'react';import ReactDOM from 'react-dom/client';

const myElement = <h1 className="myclass">Hello World</h1>;

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);
React Components
Là đoạn mã độc lập và có thể tái sử dụng. Chúng có mục đích như các hàm Javascript nhưng hoạt động riêng biệt và trả về HTML.
Component có hai loại: Class components và Function components.
Hiện tại người ta đề xuất sử dụng Function components cùng với Hooks.
Class components

import React from "react";
import ReactDOM from "react-dom/client";

class Car extends React.Component {
  render() {
    return <h2>Hi, I am a Car!</h2>;
  }
}

const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(<Car/>);
Functions components

import React from "react";
import ReactDOM from "react-dom/client";

function Car() {
    return <h2>Hi, I am a Car!</h2>;
}

const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(<Car/>);


import React from "react";
import ReactDOM from "react-dom/client";

function Greet() {
    return <p>Good Morning</p>
}

function Name(){
    return (
        <>
            <Greet/>
            <p>My Name is John Doe</p>
            <p>welcome to VietNam</p>
        </>
    );

}
const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(<Name/>);

Trong file Car.js

function Car() {
  return <h2>Hi, I am a Car!</h2>;}

export default Car;
import React from 'react';
import ReactDOM from 'react-dom/client';import Car from './Car.js';

const root = ReactDOM.createRoot(document.getElementById('root'));

root.render(<Car />);
Ví dụ
import React from "react";
import ReactDOM from "react-dom/client";

function Poem(){
  return <pre>
    <i>khi</i> con <mark>tu hú</mark> gọi bầy
    <b>lúa</b> chiêm đang chín trái cây ngọt dần
  </pre>;
}

function Form(){
  return (
    <>
      <p>H<sub>2</sub>+X<sup>2</sup></p>
    </>
  )
}

const results = <>
  <Poem/>
  <Form/>
</>

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(results)

Props
Là các đối số được truyền vào các thành phần React. Props được truyền vào các thành phần thông qua các thuộc tính HTML. Props là viết tắt của properties.

import React from "react";
import ReactDOM from "react-dom/client";

function Greet(props) {
    return <p>Good Morning, {props.fullname}</p>
}

const myE = <Greet fullname="John Doe"/>;

const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(myE);

import React from 'react';
import ReactDOM from 'react-dom/client';

function Car(props) {
  return <h2>I am a { props.brand }!</h2>;
}

function Garage() {
  const carName = "Ford";
  return (
    <>
	    <h1>Who lives in my garage?</h1>
	    <Car brand={ carName } />
    </>
  );
}
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Garage />);
Lỗi sai hay gặp:



import React from "react";
import ReactDOM from "react-dom/client";

function Car(props){
    return <li>props</li>
}
const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(<Car props="Thang" />);
import React from "react";
import ReactDOM from "react-dom/client";

function Car(props){
    return <li>{props.name}</li>
}
const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(<Car name="Thang" />);

import React from 'react';
import ReactDOM from 'react-dom/client';

function Car(props) {
  return <h2>I am a {props.color} {props.name} Car!</h2>;
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Car color="red" name="thắng" />);
state
    • Được dùng để lưu trữ và quản lý dữ liệu động của một component (thành phần). Nó cho phép component phản hồi lại các sự thay đổi (ví dụ: người dùng nhập dữ liệu, bấm nút, hoặc dữ liệu thay đổi từ phía server).
    • State là dữ liêu nội bộ của component. Component tự động render lại khi state thay đổi. Dùng khi dữ liệu có thể thay đổi theo thời gian.
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // Khai báo state

  return (
    <div>
      <p>Bạn đã bấm {count} lần</p>
      <button onClick={() => setCount(count + 1)}>
        Bấm tôi
      </button>
    </div>
  );
}

React elements
    • Sử dụng props giống như với attribute của thẻ html
    • 2 props class, for => className, htmlFor
    • Phải tuân theo quy ước có sẵn
React components
    • Sử dụng props giống như đối số cho component
    • Tự do đặt tên props
    • Đặt theo camelcase
    • Có thể bao gồm dấu gạch ngang
Chú ý:
    • Props “key” là props đặc biệt
    • Props cơ bản là đối số của component => props có thể là bất cứ kiểu dữ liệu gì
    • Sử dụng destructuring
    • Component do chúng ta định nghĩa phải viết in hoa kí tự đầu
    • Chọn component trong một object
    • Booleans, null and undefind không được render
    • Kết hợp toán tử logic để render theo điều kiện

SPA – single-Page Application (ứng dụng trang đơn hay ứng dụng một trang)
    • reactJS là 1 trang trong những thư viện tạo ra SPA
    • goohle, facebook, twitter đang sử dụng 
SPA, MPA (multi-Page Application)
SPA 
    • được cho là cách tiếp cận hiện đại hơn. 
    • Không yêu cầu tải lại trang trong quá trình sử dụng
MPA
    • là cách tiếp tận cổ điển hơn
    • tải lại trang trong quá trính sử dụng
so sánh SPA và MPA
SPA – CSR (client side rendering)
    • nhanh hơn khi sử dụng
    • phần lớn tài nguyên được tải trong lần đầu
    • trang chủ chỉ tải thêm dữ liệu mới khi cần
    • có phần font-end riêng biệt
    • không thân thiện với SEO như MPA
    • trải nghiệm trên thiết bị di động tốt hơn
    • dễ dàng tái sử dụng code
    • chia team phát triển song song
    • phát triển mobile app dễ dàng
    • phụ thuộc hoàn toàn vào Js
    • khi nhiều người sử dụng thì tốt hơn về phía sever
MPA – SSR (sever side rendering)
    • chậm hơn khi sử dụng
    • luôn tải lại trang 
    • font-end và back-end phụ thuộc vào nhau nhiều, được đặt trong cùng một dự án
    • có thể không cần Js
    • phù hợp khi không cần phát triển Web
Events
Giống như sự kiện của HTML DOM, React có thể thực hiện các hoạt động dựa trên sự kiện của người dùng.
React có cùng sự kiện với HTML.
Trình xử lý sự kiện được viết bên trong dấu ngoặc nhọn.

import React from "react";
import ReactDOM from "react-dom/client";

function Shoot(){
    const shoot = () => {
        alert("Great shot!");
    }
    return (
        <button onClick={shoot}>Take the shot!</button>
    )
}

const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(<Shoot />);

function Football() {
  const shoot = (a) => {
    alert(a);
  }

  return (
    <button onClick={() => shoot("Goal!")}>Take the shot!</button>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Football />);

import React from 'react';
import ReactDOM from 'react-dom/client';

function Football() {
  const shoot = (a, b) => {
    alert(b.type);
  }

  return (
    <button onClick={(event) => shoot("Goal!", event)}>Take the shot!</button>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Football />);
React Conditionals
function Goal(props) {
  const isGoal = props.isGoal;
  if (isGoal) {
    return <MadeGoal/>;
  }
  return <MissedGoal/>;
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Goal isGoal={false} />);


function Garage(props) {
  const cars = props.cars;
  return (
    <>
      <h1>Garage</h1>
      {cars.length > 0 &&
        <h2>
          You have {cars.length} cars in your garage.
        </h2>
      }
    </>
  );
}

const cars = ['Ford', 'BMW', 'Audi'];
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Garage cars={cars} />);

function Goal(props) {
  const isGoal = props.isGoal;
  return (
    <>
      { isGoal ? <MadeGoal/> : <MissedGoal/> }
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Goal isGoal={false} />);
React Lists
Trong React, bạn sẽ hiển thị danh sách bằng một số loại vòng lặp.

import React from "react";
import ReactDOM from "react-dom/client";

function Car(props){
    return <li>{props.name}</li>
}

function Box(){
    const transportations = ["bike", "bus", "car", "train"];
    return (
        <ul>
            {transportations.map((n) => <Car name={n} />)}
        </ul>
    )
}

const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(<Box/>);
React Forms
React sử dụng biểu mẫu để cho phép người dùng tương tác với trang web.
React Router
Tạo ứng dụng React không bao gồm định tuyến trang. React Router là giải pháp phổ biến nhất.
Để thêm React Router vào ứng dụng của bạn, hãy chạy lệnh này trong terminal từ thư mục gốc của ứng dụng.
npm I –D react-router-dom
hoặc
npm i –D react-router-dom@latest
React Memo
Sử dụng momo sẽ khiến React bỏ qua việc render một thành phần nếu props của nó không thay đổi. Điều này có thể cải thiện hiệu suất.
React CSS Styling
Có rất nhiều cách để định dạng React bằng CSS. 
React Sass Styling
Là một bộ tiền xử lý CSS, được thực thi trên máy chủ và gửi CSS đến trình duyệt.
Để cài đặt sass: npm i sass
React Hooks
Hooks đã được thêm vào React trong phiên bản 16.8
Hooks cho phép các thành phần hàm cos quyền truy cập vào trạng thái và các tính năng React khác. Vì lý do này, các thành phần lớp thường không cần thiết nữa.
Hook thường thay thế các thành phần lớp, nhưng không có hoạch xóa lớp khỏi React.
useState
Cho phép chúng ta theo dõi trạng thái trong một thành phần hàm.
Trạng thái thường đề cập đến dữ liệu hoặc thuộc tính cần theo dõi trong một ứng dụng.
useEffect
Cho phép bạn thực hiện các hiệu ứng phụ trong các thành phần của mình như là lấy dữ liệu, cập nhật trực tiếp DOM và bộ đếm thời gian.
useEffect chấp nhận 2 đối số. Đối số thứ 2 tùy chọn.
useEffect(<function>, <dependency>)	
useContent
useRef
useReducer
useMemo
Custom Hooks
map()
Dùng để lặp qua một mảng và hiển thị danh sách các phần tử trên giao diện.
Cú pháp: 
array.map((item, index) => {
  return <JSX_element />;
});
key={index}
Khi bạn render danh sách bằng .map(), bạn phải thêm các thuộc tính key để giúp React nhận biết và theo dõi các phần tử trong danh sách một cách hiệu quả.
React dùng key để biết phần tử nào thay đổi, thêm hoặc xóa khi render, tăng hiệu suất cập nhật DOM ảo
Ví dụ
Menu 1 cấp 
App.js
index.js
import React from "react";
import Menu from './index';
function App(){
  return (
    <div>
      <Menu />
      <h1>Nội dung chính</h1>
    </div>
  );
}

export default App;

import React from "react";
import ReactDom from 'react-dom/client'
import App from "./App";
const MenuItems = [
  {label: "Trang Chủ", link: '/'},
  {label: "Giới Thiệu", link: '/about'},
  {label: "Sản phẩm", link: '/products'},
  {label: "Liên Hệ", link: '/contact'}
];

const Menu = () => {
  return (
    <nav>
      <ul style={styles.menu}>
        {MenuItems.map((item, index) => (
          <li key={index} style={styles.MenuItems}>
            <a href={item.link} style={styles.link}>{item.label}</a>
          </li>
        ))}
      </ul>
    </nav>
  );
};

const styles = {
  menu: {
    display: 'flex',
    listStyle: 'none',
    padding: 0,
    margin: 0,
    backgroundColor: '#333'
  },
  MenuItems: {
    padding: '10px 20px',
  },
  link: {
    color: 'white',
    textDecoration: 'none',
  },
};

export default Menu;

const root = ReactDom.createRoot(document.getElementById('root'));
root.render(<App/>)
React Exercises