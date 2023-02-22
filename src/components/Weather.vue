<template>
    <div class="weather-container">
      <form @submit.prevent="getWeather" class="weather-form">
        <input type="text" v-model="city" placeholder="Digite a cidade" class="weather-input">
        <button type="submit" class="weather-button">Get Weather</button>
      </form>
  
      <div v-if="error" class="error">
        Ops, algo deu errado. Tente novamente mais tarde.
      </div>
  
      <weather-info v-if="weather" :weather="weather" />
    </div>
</template>
  
  
<script>
import WeatherInfo from './WeatherInfo.vue';

export default {
  components: {
    WeatherInfo
  },
  data() {
    return {
      city: '',
      error: null,
      weather: null
    }
  },
  methods: {
    async getWeather() {
      try {
        const response = await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=c3b562f902c27e1208f1a0d9dbe2131e&units=metric`);
        if (!response.ok) {
          throw new Error('City not found');
        }
        const data = await response.json();
        this.weather = data;
        this.error = null;
      } catch (error) {
        this.error = error.message;
        this.weather = null;
      }
    }
  },
  watch: {
    city() {
      this.error = null;
      this.weather = null;
    }
  },
  props: {
  }
}
</script>


<style>
.weather-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.weather-form {
  display: flex;
  align-items: center;
}
.weather-input {
  padding: 10px;
  border: none;
  border-radius: 4px;
  margin-right: 10px;
}
.weather-button {
  padding: 10px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.weather-button:hover {
  background-color: #3e8e41;
}
</style>
