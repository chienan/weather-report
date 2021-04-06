<template>
  <div id="wrapper">
    <div class="container d-flex justify-content-center">
      <div class="content-wrapper">
        <div class="nav px-4 py-4">
          <div class="nav-title">
            Weather Report
            <!-- <i
              class="fas fa-sun switch-mode"
              v-if="!lightMode"
              @click="lightMode = !lightMode"
            ></i>-->
            <!-- <i class="fas fa-moon switch-mode" v-else @click="lightMode = !lightMode"></i> -->
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

          <div class="location-section">{{weather.city.name}}</div>
          <!-- <button v-if="!lightMode" @click="lightMode = !lightMode">Light mode</button>
          <button v-else @click="lightMode = !lightMode">Dark mode</button>-->
        </div>

        <!-- weather card group -->
        <div class="card-group">
          <div class="main-card">
            <div class="date">{{weather.list[0].dt_txt}}</div>
            <div class="temperature">{{Math.round(weather.list[0].main.temp)}}°C</div>
            <div class="icon-wrapper">
              <i :class="getIcon()"></i>
            </div>
            <div class="weather" id="weather">{{weather.list[0].weather[0].main}}</div>
          </div>

          <div
            class="sub-card-group d-flex flex-wrap justify-content-around"
            v-for="(li, index) in filteredDateData"
            :key="index"
          >
            <div class="sub-card">
              <div class="sub-date">{{li.dt_txt}}</div>
              <div class="sub-temperature">{{Math.round(li.main.temp)}}°C</div>
              <i :class="filteredIcon()"></i>
              <div class="weather">{{li.weather[0].main}}</div>
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
      api_key: process.env.VUE_APP_API_KEY,
      BASE_URL: "http://api.openweathermap.org/data/2.5/",
      query: "HsinChu",
      weather: {
        city: {},
        list: []
      },
      date: "",
      location: "",
      // lightMode: false,
      filteredDateData: [],
      filteredIconDate: []
    };
  },
  methods: {
    async fetchWeather() {
      const data = await fetch(
        `${this.BASE_URL}forecast?q=${this.query}&units=metric&appid=${this.api_key}`
      );
      this.weather = await data.json();
      this.filteredDate();
      this.getIcon();
    },
    filteredDate() {
      this.filteredDateData = this.weather.list.slice(1, 5);
      this.filteredIconDate = this.weather.list.slice(1, 5);
    },
    filteredIcon() {
      const subWeather = this.filteredIconDate.shift();
      if (subWeather !== undefined) {
        // const subWeather = this.filteredIconDate.slice(0, index);

        console.log("get filtered icon");
        console.log(subWeather);

        //  const subWeatherWord = this.filteredDateData[i].weather[0].main;
        const subWeatherWord = subWeather.weather[0].main;
        console.log(subWeatherWord);

        if (subWeatherWord === "Clear") {
          return "fas fa-sun sub-icon";
        } else if (subWeatherWord === "Clouds") {
          return "fas fa-cloud sub-icon";
        } else if (subWeatherWord === "Rain") {
          return "fas fa-cloud-showers-heavy sub-icon";
        } else {
          return "far fa-snowflake sub-icon";
        }
      }
    },

    locationSubmit() {
      this.query = this.location;
      this.fetchWeather();
    },
    getIcon() {
      const weatherWord = this.weather.list[0].weather[0].main;
      if (weatherWord === "Clear") {
        return "fas fa-sun sub-icon";
      } else if (weatherWord === "Clouds") {
        return "fas fa-cloud sub-icon";
      } else if (weatherWord === "Rain") {
        return "fas fa-cloud-showers-heavy sub-icon";
      } else {
        return "far fa-snowflake sub-icon";
      }
    }
  },
  // watch: {
  //   lightMode: function() {
  //     localStorage.setItem("lightMode", JSON.stringify(this.lightMode));
  //   }
  // },
  created() {
    this.lightMode = JSON.parse(localStorage.getItem("lightMode"));
    this.fetchWeather();
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
      width: 100%
      display: flex
      flex-direction: column
      font-size: 2rem
      color: $middleblue
      .switch-mode:hover
        cursor: pointer

      .search-section
        display: flex
        .search-input
          width: 50%
          background: transparent
          border: 1px solid $lightblue
          color: $lightblue

      .location-section
        display: flex
        justify-content: center

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
      font-size: 5rem
    .icon
      font-size: 5rem

  .sub-card-group
    width: 65vw
    // height: 10vw

    .sub-card
      min-height: 220px
      min-width: 125px
      @extend %card-style
      .sub-temperature
        font-size: 2rem
      .sub-icon
        font-size: 3rem

.theme-light

  .container
    background-color: $backgroundlight
    color: $darkblue

    .main-card
      border: 2px solid $darkblue
      color: $darkblue

    .sub-card-group
      background: $backgroundlight

    .sub-card
      border: 2px solid $darkblue
      color: $darkblue

@media screen and (max-width: 550px)
  // .nav
  //   height: 5%
  //   font-size: 1rem

  .container
    width: 100vw

  .card-group
    display: flex
    flex-direction: column
    .main-card
      width: 50vw
      height: 30vw
</style>
