<script>
import axios from "axios";

export default {
  components: {},
  data() {
    return {
      city: "",
      error: "",
      info: null,
    };
  },
  computed: {
    cityName() {
      return "'" + this.city + "'";
    },
    showName() {
      return this.info.name;
    },
    showTemp() {
      return this.info.main.temp;
    },
    showFeelsLikes() {
      return this.info.main.feels_like;
    },
    showMinTemp() {
      return this.info.main.temp_min;
    },
    showMaxTemp() {
      return this.info.main.temp_max;
    },
  },
  methods: {
    getWeather() {
      if (this.city.trim().length < 2) {
        this.error = "Введите корректное название";
        return false;
      }
      this.error = "";
      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=111310c85fc97752bc1055285d67aca6`
        )
        .then((res) => (this.info = res.data));
    },
  },
};
</script>

<template>
  <div class="app">
    <h1 class="title">Погода</h1>
    <p class="text">
      Узнать погоду в {{ city === "" ? "вашем городе" : cityName }}
    </p>
    <input
      class="input"
      v-model="city"
      type="text"
      placeholder="Название города..."
    />
    <p class="error">{{ error }}</p>
    <button class="btn" @click="getWeather">Найти</button>
    <div class="info" v-if="info != null">
      <h2 class="info_content name">{{ showName }}</h2>
      <p class="info_content">
        <span class="temp">Температура:</span> {{ showTemp }}
      </p>
      <p class="info_content">
        <span class="feels">Ощущается как:</span> {{ showFeelsLikes }}
      </p>
      <p class="info_content">
        <span class="min">Минимальная температура:</span> {{ showMinTemp }}
      </p>
      <p class="info_content">
        <span class="max">Максимальная температура:</span> {{ showMaxTemp }}
      </p>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import "./assets/styles/main.scss";

.info_content {
  font-weight: 700;
  font-size: 26px;
  color: $error-color;
}

.info {
  display: flex;
  flex-direction: column;
  background-color: $white;
  border-radius: 20px;
  height: 200px;
  width: 500px;
  padding: 20px;
  & .name {
    color: $bg-color;
    font-size: 36px;
    margin-bottom: 30px;
    text-decoration: underline;
  }
  & .temp {
    color: $bg-color;
    font-size: 24px;
  }
  & .feels {
    color: $bg-color;
    font-size: 18px;
  }
  & .min {
    color: $bg-color;
    font-size: 18px;
  }
  & .max {
    color: $bg-color;
    font-size: 18px;
  }
}

.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  padding: 20px;
  width: 1000px;
  height: 700px;
  border-radius: 50px;
  background: rgb(250, 157, 0);
  background: linear-gradient(
    100deg,
    rgba(250, 157, 0, 1) 0%,
    rgba(154, 138, 0, 1) 100%
  );
  & .info {
    color: $white;
    font-size: 18px;
    margin-top: 50px;
    font-weight: 400;
  }
  & .error {
    font-size: 20px;
    margin-top: 30px;
    font-weight: 700;
    color: $error-color;
    text-transform: uppercase;
  }
  & .title {
    font-size: 50px;
    margin-top: 30px;
    font-weight: 700;
    text-transform: uppercase;
  }
  & .text {
    font-size: 22px;
    margin-top: 30px;
    font-weight: 400;
  }
  & .input {
    height: 40px;
    width: 600px;
    border: none;
    padding: 5px;
    font-size: 20px;
    margin-top: 30px;
    border-radius: 14px;
    color: rgba(0,5,29,1);
    background-color: $white;
    transition: all 0.1s ease-in;
    &:focus {
      outline: none;
      border: none;
      transform: scale(1.03);
    }
  }
  & .btn {
    border: none;
    outline: none;
    font-size: 20px;
    cursor: pointer;
    margin-top: 30px;
    padding: 14px 30px;
    color: $white;
    border-radius: 10px;
    background-color: $white;
    text-transform: lowercase;
    transition: all 0.1s ease-in;
    background: $error-color;
    background: linear-gradient(
      100deg,
      $error-color 10%,
      $error-color 100%
    );
    &:hover {
      transform: scale(1.05);
    }
  }
}
</style>
