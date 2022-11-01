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
- cara menggunakan react router
  1. install reactrouter, ada dialam folder project
  2. import browser router di main.js
  3. routes : untuk nampung loopingan yang ada
  4. import routes di app.jsx
### Params Router
- params router : fungsinya untuk mengirim sebuah parameter lewat loopingan
buat detailpage
import detailpage di app
:id : mengirim parameter
Pindah2 halaman pakai use navigate

Buat pages baru about student
About teacher
Nested router
Pakai outlet : untuk nampilin anak2 di about
Import outlet
Panggil outlet di aboutpage
