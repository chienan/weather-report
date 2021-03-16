<template>
  <div class="container d-flex justify-content-center">
    <div class="content-wrapper">
      <div class="nav">Weather Report</div>

      <div class="card-group d-flex justify-content-center align-items-center">
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
  </div>
</template>

<style lang="sass" scoped>
@import "../assets/scss/main.scss"

.container
  width: 100%
  height: 100%

  .content-wrapper
    width: 85%
    .nav
      height: 45px
      width: 100%

.card-group
  min-height: 450px

  .main-card
    width: 35%
    height: 40%
    max-width: 350px
    min-height: 200px
    @extend %main-card-style
    .temperature
      font-size: 3rem

  .sub-card-group
    width: 65%
    height: 20%

    .sub-card
      min-height: 250px
      min-width: 100px
      @extend %card-style
</style>
