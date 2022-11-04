# Writing-Week-6
## Prop Types
- prop types untuk mencegah kesalahan yang tidak diinginkan
- cara menggunakan prop types : 
  1. install prop types pada terminal
  2. ketik npm install prop-types pada terminal
  3. import prop-types di component
  ```jsx
  import PropTypes from "prop-types";
  ```
- jika ada kesalahan pada type data, maka prop-types akan memberitahu bahwa terjadi error di console
- type data string
```jsx
StudentInfo.propTypes = {
  name: PropTypes.string,
};
```
- type data number
```jsx
StudentInfo.propTypes = {
  age: PropTypes.number,
};
```
- type data any
```jsx
StudentInfo.propTypes = {
  name: PropTypes.any.isRequired, //isRequired data harus ada
};
```
- memberikan opsi untuk type data
```jsx
StudentInfo.propTypes = {
  age: PropTypes.oneOfType([PropTypes.string, PropTypes.number]), 
};
```
- type data array
```jsx
StudentInfo.propTypes = {
  data: PropTypes.array, 
};
```
- mengecek value dari props
```jsx
StudentInfo.propTypes = {
  data: PropTypes.arrayOf(PropTypes.number), 
};
```
- array dengan berbagai macam type data
```jsx
StudentInfo.propTypes = {
  data: PropTypes.arrayOf(PropTypes.oneOfType[PropTypes.number, PropTypes.string]), 
};
- type data object
```jsx
StudentInfo.propTypes = {
  info: PropTypes.shape({
    hobby: PropTypes.string,
    class: PropTypes.number,
  }), 
};
```
- mengecek nilai dan key dari object
```jsx
StudentInfo.propTypes = {
  info: PropTypes.exact({
    hobby: PropTypes.string,
    class: PropTypes.number,
  }).isRequired, 
};
```
## React Router
- router : fungsi router untuk pindah2 halaman
- keunggulan router daripada tag a pada html adalah lebih cepat ketika berpindah halamn, tidak perlu refresh lama halaman
- cara menggunakan react router
  1. install react router didalam folder project
  ```jsx
  npm install reat-roter-dom
  ```
  2. import browser router di main.jsx
  ```jsx
  //main.jsx
  import { BrowserRouter } from "react-router-dom";
  ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>
  );
  ```
  3. import routes di app.jsx. routes : untuk nampung loopingan yang ada
  ```jsx
  //app.jsx
  import { Routes, Route, Link } from "react-router-dom";
  const App = () => {
  return (
    <>
      <nav>
        <Link to={"/"}>Home |</Link>  //Link seperti tag a pada html
        <Link to={"/about"}>About</Link>
      </nav>
      
      <Routes>
        <Route path="/" element={<HomePage />} />   //halaman pertama yang dimunculkan hanya diberi "/"
        <Route path="/detail/:id" element={<DetailPage />} />
      </Routes>
    </>
  );
  };

  export default App;       
  ```
### Params Router
- params router : fungsinya untuk mengirim sebuah parameter lewat loopingan
- cara menggunakan params
  1. buat folder (dengan nama detailpage)
  2. import detailpage di app.jsx
  ```jsx
  //app.jsx
  import DetailPage from "./pages/DetailPage";
  const App = () => {
  return (
    <>
      </Routes>
      <Route path="/detail/:id" element={<DetailPage />} /> // :id adalah untuk mengirim parameter
      </Routes>
    </>
  );
  };

  export default App;
  ```
  ```jsx
  //detailpage.jsx
  import { useParams } from "react-router-dom";

  const DetailPage = () => {
  // useParams untuk menangkap id yang kita kirim dari halaman home
  const { id } = useParams();
  console.log(id);

  const detailInfo = [
    {
      id: 1,
      name: "Mika",
      address: "jakarta",
      hobby: "menari",
    },
    {
      id: 2,
      name: "Reyhan",
      address: "bandung",
      hobby: "memancing",
    },
    {
      id: 3,
      name: "Asep",
      address: "malang",
      hobby: "membaca",
    },
  ];
  // 1. filter data dari detailInfo dan dicocokkan dengan id yg kita kirim dari home (yang ditangkap di params)
  // 2. Mapping data untuk menampilkan hasil yang sesuai dari data filter
  return (
    <>
      {detailInfo
        .filter((el) => el.id === +id)
        .map((el) => {
          return (
            <div key={el.id}>
              <h2>Name: {el.name}</h2>
              <h2>Address: {el.address}</h2>
              <h2>Hobby: {el.hobby}</h2>
            </div>
          );
        })}
    </>
  );
  };

  export default DetailPage;
  ```
- Pindah2 halaman pakai use navigate
```jsx
import { useNavigate, Link } from "react-router-dom";

const HomePage = () => {
  // panggil useNavigate agar bisa digunakan pada function handleDetail
  const navigation = useNavigate();
  let data = [
    {
      id: 1,
      name: "Mika",
    },
    {
      id: 2,
      name: "Reyhan",
    },
    {
      id: 3,
      name: "Asep",
    },
  ];

  const handleDetail = (id) => {
    // untuk pindah halaman ke page detail sekaligus membawa id params
    navigation(`/detail/${id}`);
  };
  return (
    <>
      <h1>Ini Home Page</h1>
      {data.map((el) => {
        return (
          <div key={el.id}>
            <h2>Nama: {el.name}</h2>
            <button onClick={() => handleDetail(el.id)}>Detail</button>
          </div>
        );
      })}
      <Link to={"about/student"}>About Student |</Link>
      <Link to={"about/teacher"}>About Teacher</Link>
    </>
  );
};

export default HomePage;
```
### Nested router
- cara menggunakan nested router
  1. Buat folder baru
  ```jsx
  //app.jsx
  import { Routes, Route, Link } from "react-router-dom";
  import AboutStudent from "./pages/AboutStudent";
  import AboutTeacher from "./pages/AboutTeacher";
  import AboutSchool from "./pages/AboutSchool";
  const App = () => {
  return (
    <>
       <Routes>
         <Route path="/about" element={<AboutPage />}>
          <Route path="student" element={<AboutStudent />} />
          <Route path="teacher" element={<AboutTeacher />} />
          <Route index element={<AboutSchool />} /> //index digunakan agar element AboutSchool langsung ditampilkan pertama kali ketika page about dibuka
       </Route>
       </Routes>
    </>
  );
  };

  export default App;
  ```jsx 
  //aboutschool.jsx
  const AboutSchool = () => {
  return (
    <>
      <h1>About School</h1>
    </>
  );
  };

  export default AboutSchool;
  ```
  ```jsx
  //aboutteacher.jsx
  const AboutTeacher = () => {
  return (
    <>
      <h1>About Teacher</h1>
    </>
  );
  };

  export default AboutTeacher;
  ```
  ```jsx
  const AboutStudent = () => {
  return (
    <>
      <h1>About Student</h1>
    </>
  );
  };

  export default AboutStudent;
  ```
- Pakai outlet : untuk nampilin anak2 di about
```jsx
import { Outlet, Link } from "react-router-dom";

const AboutPage = () => {
  return (
    <>
      <Outlet />
      <Link to={"student"}>About Student |</Link>
      <Link to={"teacher"}>About Teacher</Link>
    </>
  );
};

export default AboutPage;
```
### not-found
```jsx
//app.jsx
import NotFound from "./pages/NotFound";
const App = () => {
  return (
    <>
      <Routes>
        <Route path="*" element={<NotFound />} /> //tambahkan path="*" untuk menampilkan halaman yg tidak ditemukan. case nya adalah ketika user mengakses path tertentu yang tidak terdaftar di routingan yang kita miliki
      </Routes>
    </>
  );
};

export default App;
```
## Redux
- Untuk mengatasi props drilling, bisa menggunakan state management seperti redux, context, jotai, zustand
- redux adalah sebuah third party untuk memanipulasi state management didalam react
- Konsep redux : Akan membuat tempat terpusat, lalu ketika ada component yang membutuhkan tinggal ngambil dari tempat tersebut
### cara menggunakan React redux
1. Install redux : bisa menggunakan redux core, redux toolkit
```jsx
//ini menggunakan redux core
npm install redux
```
2. Install react redux
```jsx
npm install react-redux
```
3. install store
- Harus menyediakan storenya dahulu
```jsx
//index.js
import { createStore } from 'redux'
import keranjangReducer from '../reducer/keranjangReducer'

const store = createStore(keranjangReducer)

export default store
```
4. Buat reducer
```jsx
//KeranjangReducer.js
const initialState = {
  totalKeranjang: 0,
};
function keranjangReducer(state = initialState, action) {
  switch (action.type) {       //Action ; sebuah function yang memiliki objek property type. Action akan dikirim ke reducer
    default:state
    break;
  }
}

export default keranjangReducer;
```
5. Buat provider, menggunakan react redux di main jsx import provider
```jsx
//main.jsx
import { Provider } from 'react-redux'
```
```jsx
//main.jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import { Provider } from 'react-redux'
import App from './App'
import store from './redux/store'

ReactDOM.createRoot(document.getElementById('root')).render(
  // <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  // </React.StrictMode>
)
```
6. Buat components
```
//Counter.jsx
//Keranjang.jsx
//ListProduct.jsx
//SummaryPembelian.jsx
```
7. useSelector
```jsx
import React from 'react'
import { useSelector } from 'react-redux'

function Keranjang() {
  const {totalKeranjang} = useSelector(state => state)

  // console.log(state)

  return (
    <div>
      <span>Keranjang</span>
      <span> {totalKeranjang}</span>
    </div>
  )
}

export default Keranjang
```
8. useDispatch
- Dispatch : mengirim action ke dalam reducer
```jsx
//Counter.jsx
import { useDispatch } from "react-redux";
```
### Combine Reducer
- Combine Reducer : agar bisa menampung banyak store
- karena createStore hanya bisa menampung 1 store
```jsx
//index.jsx
import { combineReducers, createStore } from "redux";
import counterReducer from "../reducer/counterReducer";
import todoReducer from "../reducer/todoReducer";

const allReducer = combineReducers({
  counter: counterReducer,
  todo: todoReducer
})

const store = createStore(allReducer);

export default store;
```
