<template>
  <div id="wrapper" :class="{ 'theme-light': lightMode }">
    <div class="main-content">
      <div class="container d-flex justify-content-center">
        <div class="content-wrapper">
          <div class="nav px-4 py-4">
            <div class="nav-title">
              Weather Report
              <i
                class="fas fa-sun switch-mode"
                v-if="!lightMode"
                @click="lightMode = !lightMode"
              ></i>
              <i class="fas fa-moon switch-mode" v-else @click="lightMode = !lightMode"></i>
            </div>

            <div class="nav-search">
              <form>
                <div class="search-section py-4">
                  <label for="search" class="search"></label>
                  <input
                    type="place"
                    class="form-control search-input"
                    id="search"
                    placeholder="search for a place"
                    v-model="location"
                  />
                  <button
                    type="submit"
                    class="btn btn-primary mx-4"
                    @click.stop.prevent="locationSubmit"
                  >search</button>
                </div>
              </form>
            </div>

            <!-- <button v-if="!lightMode" @click="lightMode = !lightMode">Light mode</button>
            <button v-else @click="lightMode = !lightMode">Dark mode</button>-->
          </div>

          <div class="card-group">
            <div class="main-card">
              <div class="location-section">{{weather.name}}</div>

              <div class="date">{{currentDate}}</div>
              <div class="temperature">{{Math.round(weather.main.temp)}}°C</div>
              <div class="icon-wrapper">
                <i :class="getIcon()"></i>
              </div>
              <div class="weather" id="weather">{{weather.weather[0].main}}</div>
            </div>
          </div>
        </div>
        <!-- <link rel="stylesheet" href="<%= BASE_URL %>css/lighttheme.css" /> -->
      </div>
    </div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  data: () => {
    return {
      api_key: process.env.VUE_APP_API_KEY,
      BASE_URL: "http://api.openweathermap.org/data/2.5/",
      query: "HsinChu",
      weather: {},
      date: "",
      location: "",
      lightMode: false
    };
  },
  methods: {
    async fetchWeather() {
      const data = await fetch(
        `${this.BASE_URL}weather?q=${this.query}&units=metric&appid=${this.api_key}`
      );
      this.weather = await data.json();
      this.getIcon();
    },
    locationSubmit() {
      this.query = this.location;
      this.fetchWeather();
    },
    getIcon() {
      const weatherWord = this.weather.weather[0].main;
      if (weatherWord === "Clear") {
        return "fas fa-sun icon";
      } else if (weatherWord === "Clouds") {
        return "fas fa-cloud icon";
      } else if (weatherWord === "Rain") {
        return "fas fa-cloud-showers-heavy icon";
      } else {
        return "far fa-snowflake icon";
      }
    }
  },
  computed: {
    currentDate() {
      return moment().format("MMMM Do YYYY");
    }
  },
  watch: {
    lightMode: function() {
      localStorage.setItem("lightMode", JSON.stringify(this.lightMode));
    }
  },
  created() {
    this.lightMode = JSON.parse(localStorage.getItem("lightMode"));
    this.fetchWeather();
  }
};
</script>

<style lang="sass">
@import "../assets/scss/main.scss"
@import url('https://use.fontawesome.com/releases/v5.8.1/css/all.css')

// #wrapper
//   background-color: $darkblue

// #wrapper ~.theme-light
//   background-color: $lightblue

.main-content
  background-color: $darkblue

.container
  width: 100%
  height: 100vw
  background-color: $darkblue

  .content-wrapper
    width: 85%
    .nav
      width: 100%
      display: flex
      flex-direction: column
      font-size: 2rem
      color: $middleblue
      .nav-title
        display: flex
        justify-content: center

      .switch-mode:hover
        cursor: pointer

      .search-section
        display: flex
        align-items: center
        justify-content: center
        .search-input
          width: 40%
          background: transparent
          border: 1px solid $lightblue
          color: $lightblue

.card-group
  min-height: 450px
  display: flex
  justify-content: center
  align-items: center

  .main-card
    width: 30vw
    max-width: 250px
    min-height: 350px
    min-width: 250px
    @extend %main-card-style

    .temperature
      font-size: 5rem
    .icon
      font-size: 3rem
    .location-section
      display: flex
      justify-content: center
      font-size: 20px

.theme-light
  .main-content
    background-color: $backgroundlight

    background-color: $backgroundlight

  .container
    background-color: $backgroundlight
    color: $middleblue

    .main-card
      border: 2px solid $middleblue
      color: $middleblue
</style>
