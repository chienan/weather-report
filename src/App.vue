<template>
  <div id="weather-report">
    <router-view />
  </div>
</template>

<style lang="sass">
@import "/assets/scss/main.scss"
@import url('https://fonts.googleapis.com/css2?family=Ubuntu:ital,wght@0,300;1,400&display=swap')

body
  margin: 0
  padding: 0

*
  box-sizing: border-box
  font-family: 'Ubuntu', sans-serif

h1,
h2,
h3,
h4,
h5,
h6,
p
  margin: 0px
  padding: 0px

ul,
ol,
li
  list-style: none
  margin: 0px
  padding: 0px

a,
a:hover,
a:focus
  text-decoration: none

img
  display: block
  object-fit: cover

.btn,
button,
button:focus,
input:focus,
textarea:focus,
select,
select:focus,
a:focus
  outline: 0px !important

button
  background-color: transparent
  border: 0
  cursor: pointer

button[disabled]
  pointer-events: none
</style>
