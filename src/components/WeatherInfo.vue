<template>
    <div>
      <h2>{{ weather.name }}, {{ weather.sys.country }}</h2>
      <div class="weather-info">
        <p>{{ weather.main.temp }} °C</p>
        <p>{{ weather.weather[0].description }}</p>
        <p>Umidade: {{ weather.main.humidity }}</p>
        <p>Vento: {{ weather.wind.speed }}</p>
      </div>
    </div>
</template>
  
<script>
  export default {
    name: 'WeatherInfo',
    props: {
      weather: {
        type: Object,
        required: true
      }
    }
  }
</script>

<style>
.weather-info {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #fafafa;
  border-radius: 4px;
  padding: 20px;
  box-shadow: 0px 1px 3px rgba(0, 0, 0, 0.2);
  margin-top: 20px;
}

.weather-info p {
  margin: 10px 0;
}
</style>

  