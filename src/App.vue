<template>
  <div
    id="app"
    :class="
      typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''
    "
  >
    <main
      :class="
        typeof weather.main != 'undefined' && weather.weather[0].main == 'Rain'
          ? 'rain'
          : ''
      "
    >
      <div class="search-box">
        <input
          v-model="query"
          type="text"
          class="search-bar"
          placeholder="Search..."
          @keypress="fetchWeather"
        />
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">
            {{ weather.name }}, {{ weather.sys.country }}
          </div>
          <div class="date">{{ dateBuilder }}</div>
        </div>
        <div class="weather-box">
          <Snow
            v-if="typeof weather.main != 'undefined' && weather.main.temp <= 1"
          />
          <!-- <Rain v-if="typeof weather.main != 'undefined' && weather.weather[0].main == 'Rain'" /> -->
          <div
            class="sun"
            v-if="
              typeof weather.main != 'undefined' &&
              weather.main.temp >= 16 &&
              weather.weather[0].main != 'Rain'
            "
          >
            <svg
              class="sun-icon"
              xmlns="http://www.w3.org/2000/svg"
              version="1.1"
              x="0px"
              y="0px"
              viewBox="0 0 43.4 43.4"
              enable-background="new 0 0 43.4 43.4"
              xml:space="preserve"
            >
              <circle
                class="circle"
                fill="none"
                stroke="#252223"
                stroke-width="2"
                stroke-miterlimit="10"
                cx="21.7"
                cy="21.5"
                r="12.6"
              />
              <line
                class="ray"
                fill="none"
                stroke="#252223"
                stroke-width="2"
                stroke-miterlimit="10"
                x1="21.7"
                y1="6.3"
                x2="21.7"
                y2="0"
              />
              <line
                class="ray"
                fill="none"
                stroke="#252223"
                stroke-width="2"
                stroke-miterlimit="10"
                x1="21.7"
                y1="43.4"
                x2="21.7"
                y2="37"
              />
              <line
                class="ray"
                fill="none"
                stroke="#252223"
                stroke-width="2"
                stroke-miterlimit="10"
                x1="6.3"
                y1="21.7"
                x2="0"
                y2="21.7"
              />
              <line
                class="ray"
                fill="none"
                stroke="#252223"
                stroke-width="2"
                stroke-miterlimit="10"
                x1="43.4"
                y1="21.7"
                x2="37"
                y2="21.7"
              />
              <line
                class="ray"
                fill="none"
                stroke="#252223"
                stroke-width="2"
                stroke-miterlimit="10"
                x1="10.8"
                y1="10.8"
                x2="6.4"
                y2="6.4"
              />
              <line
                class="ray"
                fill="none"
                stroke="#252223"
                stroke-width="2"
                stroke-miterlimit="10"
                x1="37"
                y1="37"
                x2="32.5"
                y2="32.5"
              />
              <line
                class="ray"
                fill="none"
                stroke="#252223"
                stroke-width="2"
                stroke-miterlimit="10"
                x1="10.8"
                y1="32.5"
                x2="6.4"
                y2="37"
              />
              <line
                class="ray"
                fill="none"
                stroke="#252223"
                stroke-width="2"
                stroke-miterlimit="10"
                x1="37"
                y1="6.4"
                x2="32.5"
                y2="10.8"
              />
              <line
                class="ray"
                fill="none"
                stroke="#252223"
                stroke-width="2"
                stroke-miterlimit="10"
                x1="15.6"
                y1="7.6"
                x2="13.2"
                y2="1.8"
              />
              <line
                class="ray"
                fill="none"
                stroke="#252223"
                stroke-width="2"
                stroke-miterlimit="10"
                x1="30.2"
                y1="41.6"
                x2="27.7"
                y2="35.8"
              />
              <line
                class="ray"
                fill="none"
                stroke="#252223"
                stroke-width="2"
                stroke-miterlimit="10"
                x1="7.6"
                y1="27.7"
                x2="1.8"
                y2="30.2"
              />
              <line
                class="ray"
                fill="none"
                stroke="#252223"
                stroke-width="2"
                stroke-miterlimit="10"
                x1="41.6"
                y1="13.2"
                x2="35.8"
                y2="15.6"
              />
              <line
                class="ray"
                fill="none"
                stroke="#252223"
                stroke-width="2"
                stroke-miterlimit="10"
                x1="7.4"
                y1="16"
                x2="1.6"
                y2="13.6"
              />
              <line
                class="ray"
                fill="none"
                stroke="#252223"
                stroke-width="2"
                stroke-miterlimit="10"
                x1="41.8"
                y1="29.7"
                x2="35.9"
                y2="27.4"
              />
              <line
                class="ray"
                fill="none"
                stroke="#252223"
                stroke-width="2"
                stroke-miterlimit="10"
                x1="16"
                y1="35.9"
                x2="13.6"
                y2="41.8"
              />
              <line
                class="ray"
                fill="none"
                stroke="#252223"
                stroke-width="2"
                stroke-miterlimit="10"
                x1="29.7"
                y1="1.6"
                x2="27.4"
                y2="7.4"
              />
            </svg>
          </div>
          <div class="weather-box-details">
            <div class="weather-temp">
              <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
            </div>
            <div class="weather-details">
              <p>
                <span>Feels like:</span>
                {{ weather.main.feels_like }}
              </p>
              <p>
                <span>Humidity:</span>
                {{ weather.main.humidity }}%
              </p>
              <p>
                <span>Pressure:</span>
                {{ weather.main.pressure }}
              </p>
              <p>
                <span>Temp max:</span>
                {{ weather.main.temp_max }}°c
              </p>
              <p>
                <span>Temp min:</span>
                {{ weather.main.temp_min }}°c
              </p>
              <p>
                <span>Wind:</span>
                {{ weather.wind.speed }}km/h
              </p>
            </div>
          </div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
      <div v-else class="intro">
        <h1>Prepare for your week ahead with our weather app</h1>
        <p>Search for weather in your city!</p>
      </div>
      <p
        class="notFound"
        v-if="typeof weather.main == 'undefined' && !startTyping"
      >
        Sorry, but we didn't found anything..
      </p>
    </main>
  </div>
</template>

<script>
import Snow from "./components/Snow";
export default {
  components: {
    Snow,
  },
  data() {
    return {
      api_key: "4eaa28fcd3fa87ee49c1d5ec0af1d794",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
      startTyping: true,
    };
  },
  methods: {
    fetchWeather(e) {
      if (e.key == "Enter") {
        this.startTyping = false;
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
    },
  },
  computed: {
    dateBuilder() {
      let d = new Date();
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} ${date} ${month} ${year}`;
    },
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  overflow: hidden;
  font-family: "montserrat", sans-serif;
}

#app {
  background-image: url("./assets/cold-bg.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
#app.warm {
  background-image: url("./assets/warm-bg.jpg");
}

main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.25),
    rgba(0, 0, 0, 0.75)
  );
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
  .search-bar {
    display: block;
    width: 100%;
    padding: 15px;
    color: #313131;
    font-size: 20px;
    appearance: none;
    border: none;
    outline: none;
    background: none;
    box-shadow: 0 0 8px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.5);
    border-radius: 0 16px 0 16px;
    transition: 0.4s;
    &:focus {
      box-shadow: 0 0 16px rgba(0, 0, 0, 0.25);
      background-color: rgba(255, 255, 255, 0.75);
      border-radius: 16px 0 16px 0;
    }
  }
}

.location-box {
  .location,
  .date {
    color: white;
    font-size: 32px;
    font-weight: 500;
    text-align: center;
    text-shadow: 1px 3px rgba(0, 0, 0, 0.45);
  }
  .date {
    font-size: 20px;
    font-weight: 300;
    font-style: italic;
  }
}

.weather-box {
  text-align: center;
  &-details {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    .temp,
    .weather-details {
      position: relative;
      display: inline-block;
      min-height: 200px;
      padding: 10px 25px;
      color: white;
      font-size: 102px;
      font-weight: 900;
      text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
      background-color: rgba(255, 255, 255, 0.25);
      border-radius: 16px;
      margin: 30px 0;
      box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
    }
    .weather-temp,
    .weather-details {
      display: flex;
      flex-direction: column;
    }
    .weather-details {
      align-items: flex-start;
      margin-left: 20px;
      span {
        font-size: 25px;
      }
      p {
        color: white;
        font-size: 20px;
        font-weight: 500;
        text-shadow: 1px 3px rgba(0, 0, 0, 0.45);
      }
    }
  }
  .weather {
    color: white;
    font-size: 48px;
    font-weight: 700;
    font-style: italic;
    text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  }
}

.intro {
  text-align: center;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  h1 {
    font-size: 30px;
  }
  h1,
  p {
    font-weight: 900;
    color: white;
    text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
    letter-spacing: 1px;
    word-spacing: 2px;
  }
  p {
    margin-top: 10px;
    font-size: 20px;
    color: rgba(241, 241, 197, 0.815);
  }
}

.notFound {
  text-align: center;
  margin: 200px auto;
  color: white;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.45);
}

.sun {
  width: 10%;
  margin: 20px auto 0;
  display: block;
  animation: rotate 10s 0s linear infinite;
  fill: #fd7c4f;
  transition: all 0.4s;
  .ray,
  .circle {
    stroke: #fdf14f;
    transition: all 0.4s;
  }
}

.rain {
  height: 100vh;
  background-image: url("./assets/rain.png");
  animation: rainAnimation 0.17s linear infinite;
  &::before {
    content: "";
    position: absolute;
    width: 100%;
    opacity: 0;
  }
}

// keyframes
@keyframes rainAnimation {
  0% {
    background-position: 0% 0%;
  }
  100% {
    background-position: 20% 100%;
  }
}

@keyframes rotate {
  0% {
    transform: rotate(0deg);
  }

  50% {
    transform: rotate(180deg);
  }

  100% {
    transform: rotate(360deg);
  }
}

@keyframes border-transform {
  0%,
  100% {
    border-radius: 63% 37% 54% 46% / 55% 48% 52% 45%;
  }
  14% {
    border-radius: 40% 60% 54% 46% / 49% 60% 40% 51%;
  }
  28% {
    border-radius: 54% 46% 38% 62% / 49% 70% 30% 51%;
  }
  42% {
    border-radius: 61% 39% 55% 45% / 61% 38% 62% 39%;
  }
  56% {
    border-radius: 61% 39% 67% 33% / 70% 50% 50% 30%;
  }
  70% {
    border-radius: 50% 50% 34% 66% / 56% 68% 32% 44%;
  }
  84% {
    border-radius: 46% 54% 50% 50% / 35% 61% 39% 65%;
  }
}
</style>
