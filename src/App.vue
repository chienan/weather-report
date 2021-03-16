<template>
  <div id="weather-report">
    <router-view />
  </div>
</template>

<style lang="scss">
// @import "bootstrap";
// @import "bootstrap/dist/css/bootstrap.min.css";

/* CSS reset */
body {
  margin: 0;
  padding: 0;
}
* {
  box-sizing: border-box;
  font-family: "Raleway", sans-serif;
}
h1,
h2,
h3,
h4,
h5,
h6,
p {
  margin: 0px;
  padding: 0px;
}

ul,
ol,
li {
  list-style: none;
  margin: 0px;
  padding: 0px;
}
a,
a:hover,
a:focus {
  text-decoration: none;
}
img {
  display: block;
  object-fit: cover;
}
.btn,
button,
button:focus,
input:focus,
textarea:focus,
select,
select:focus,
a:focus {
  outline: 0px !important;
}
button {
  background-color: transparent;
  border: 0;
  cursor: pointer;
}
button[disabled] {
  pointer-events: none;
}

// #nav {
//   padding: 30px;

//   a {
//     font-weight: bold;
//     color: #2c3e50;

//     &.router-link-exact-active {
//       color: #42b983;
//     }
//   }
// }
</style>
