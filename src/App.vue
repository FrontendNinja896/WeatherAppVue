<script>
import axios from 'axios';
export default{
  data(){
    return{
      SelectCity: "",
      info: "",
      error: ""
    }
  },
  methods:{
    KnowWeather(){
      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.SelectCity}&units=metric&appid=bde1879948e8a2113101884d2fbd3c54`)
      .then(i => (this.info = i.data.main))
    }
  },
  computed:{
    EnterCity(){
      return this.SelectCity == "" ? 'вашем городе' : this.SelectCity
    },
    Temp(){
      return "Текущая температура: " + this.info.temp
    },
    MinTemp(){
      return "Минимальная температура: " + this.info.temp_min
    },
    MaxTemp(){
      return "Максимальная температура: " + this.info.temp_max
    },
    FeelsLike(){
      return "Ощущается как:" + this.info.feels_like
    }
  }
}
</script>

<template>
  <h1 className="mt-5 text-primary fw-bolder">Погодное приложение</h1>
  <form method="post" class="wrapper mt-5">
    <h1>Погода в {{ EnterCity }}</h1>
    <input type="name" v-model="SelectCity" class="form-control"></input>
    <button disabled v-if="this.SelectCity == ''" type="button" class="btn btn-primary btn-lg mt-5">Город не указан</button>
    <button v-else type="button" class="btn btn-primary btn-lg mt-5" v-on:click="KnowWeather()">Узнать погоду</button>
    <p v-show="this.SelectCity == ''" className="fs-1 text-danger">{{ error = "Ошибка!" }}</p>
    <div v-show="this.info != ''">
      <p class="fs-2">{{ Temp }}</p>
      <p class="fs-2">{{ MinTemp }}</p>
      <p class="fs-2">{{ MaxTemp }}</p>
      <p class="fs-2">{{ FeelsLike }}</p>
    </div>
  </form>
</template>

<style scoped>
.wrapper{
  width: 500px;
  height: max-content;
  background-color: #968299;
  border-radius: 10px;
}
</style>
