<template>
 <div class="d-flex justify-content-center">
  <div class="card" style="width: 38rem;">
   <img src="./assets/city.jpg" class="card-img-top"/>
   <div class="card-body">
    <div class="input-group mb-3">
      <button class="btn btn-primary" type="button"  @click="getData">show me</button>
      <input type="text" class="form-control" placeholder="Enter the city name" style="text-align: center;" v-model="city" />
    </div>
    <div class="card-text" v-if="data">
      <p>city: {{ data.name }}</p>
      <p>temperature: {{ data.main.temp }}</p>
      <p>description: {{ data.weather[0].description }}</p>
      <p>wind speed: {{ data.wind.speed }}</p>
    </div>
    <p class="card-text" v-else-if="isLoading">
          Fetching data...
   </p>
    
  </div>
</div>
</div>
</template>
<script >
import axios from 'axios'
const API_KEY= '17ffcbd770189d6b2c3d4b30a7cbc9b2'; 

export default {
  name: "App",

  data: () => ({
    city: '',
    data: null,
    isLoading: false,
  }),

  methods: {
    getData() {
      this.isLoading = true 
      axios.get(`https://api.openweathermap.org/data/2.5/weather`,{
        params:{
          q:this.city,
          appid:API_KEY,
          units:'metric',
          lang:'eng'
        }
      }).then(({ data })=>{
        this.isLoading = false,
        this.data = data
      })
    }
  }
}
</script>
<style >

</style>
