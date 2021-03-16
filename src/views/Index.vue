<template>
  <div class="container">
    <div class="nav">Weather Report</div>

    <div class="d-flex card-group">
      <div class="main-card">
        <div class="date">Today</div>
        <div class="temperature">16°C</div>
        <div class="icon">^____^</div>
      </div>

      <div class="d-flex sub-card-group">
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
</template>

<style scoped>
@import "../assets/scss/main.scss";

* {
  border: 1px solid gray;
}

.card-group {
  width: 85%;
}
.main-card {
  width: 35%;
  height: 40%;
}
.sub-card-group {
  border: 1px solid salmon;
  width: 25%;
  height: 20%;
}

/* .main-card,
.sub-card {
} */
</style>