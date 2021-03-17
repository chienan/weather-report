<template>
  <div id="wrapper" :class="{ 'theme-light': lightMode }">
    <div class="container d-flex justify-content-center">
      <div class="content-wrapper">
        <div class="nav px-4 py-4">
          Weather Report
          <i class="fas fa-sun" v-if="!lightMode" @click="lightMode = !lightMode"></i>
          <i class="fas fa-moon" v-else @click="lightMode = !lightMode"></i>
          <!-- <button v-if="!lightMode" @click="lightMode = !lightMode">Light mode</button>
          <button v-else @click="lightMode = !lightMode">Dark mode</button>-->
        </div>

        <div class="card-group">
          <div class="main-card">
            <div class="date">Today</div>
            <div class="temperature">16°C</div>
            <div class="icon">^____^</div>
          </div>

          <div class="sub-card-group d-flex flex-wrap justify-content-around">
            <div class="sub-card">
              <div class="sub-date">Thursday</div>
              <div class="sub-temperature">25°C</div>
              <div class="sub-icon">@......@</div>
            </div>
            <div class="sub-card">
              <div class="sub-date">Thursday</div>
              <div class="sub-temperature">25°C</div>
              <div class="sub-icon">@......@</div>
            </div>
            <div class="sub-card">
              <div class="sub-date">Thursday</div>
              <div class="sub-temperature">25°C</div>
              <div class="sub-icon">@......@</div>
            </div>
            <div class="sub-card">
              <div class="sub-date">Thursday</div>
              <div class="sub-temperature">25°C</div>
              <div class="sub-icon">@......@</div>
            </div>
          </div>
        </div>
      </div>
      <!-- <link rel="stylesheet" href="<%= BASE_URL %>css/lighttheme.css" /> -->
    </div>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      lightMode: false
    };
  },
  watch: {
    lightMode: function() {
      localStorage.setItem("lightMode", JSON.stringify(this.lightMode));
    }
  },
  created() {
    this.lightMode = JSON.parse(localStorage.getItem("lightMode"));
  }
};
</script>

<style lang="sass" scoped>
@import "../assets/scss/main.scss"
@import url('https://use.fontawesome.com/releases/v5.8.1/css/all.css')

.container
  width: 100vw
  height: 100vw
  background-color: $darkblue

  .content-wrapper
    width: 85%
    .nav
      height: 15%
      width: 100%
      font-size: 2rem
      color: $middleblue

.card-group
  min-height: 450px
  display: flex
  justify-content: center
  align-items: center

  .main-card
    width: 25vw
    height: 35vw
    max-width: 250px
    min-height: 350px
    min-width: 125px
    @extend %main-card-style

    .temperature
      font-size: 3rem

  .sub-card-group
    width: 65vw
    height: 10vw

    .sub-card
      min-height: 220px
      min-width: 125px
      @extend %card-style
      .sub-temperature
        font-size: 2rem

.theme-light
  .container
    background-color: $backgroundlight
    color: $darkblue

    .main-card
      border: 2px solid $darkblue
      color: $darkblue

    .sub-card
      border: 2px solid $darkblue
      color: $darkblue

@media screen and (max-width: 550px)
  // .nav
  //   height: 5%
  //   font-size: 1rem

  .container
    width: 100vw
    height: 100vw

  .card-group
    display: flex
    flex-direction: column
    .main-card
      width: 50vw
      height: 30vw
</style>
