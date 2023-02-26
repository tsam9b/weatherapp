<template>


<div class="input-group" v-show ="!isModalVisible">
  <input type="search" class="form-control rounded"
          placeholder="Search the city..." aria-label="Search" 
          aria-describedby="search-addon" v-model="city" @input="searchCity"/>
  <!-- <button id="search-button" type="button" class="btn btn-outline-primary" @click ="searchCity">Search</button> -->
</div>

<table id="list-view" v-for="city in cityList" :key="city">
  <tr>
    <td @click ="clickCity(city)">{{city.name}} <span class="country-code">{{city.state}} ({{city.country}})</span></td>
  </tr>
</table>


<div id="app">

  <cityDetails
    :cityTitle = "cityTitle"
    :weatherDetails = "weatherDetails"
    :weatherDetailsIcon = "weatherDetailsIcon"
    :tmp = "tmp"
    :feels_like = "feels_like"
    :temp_min = "temp_min"
    :temp_max = "temp_max"
    :pressure = "pressure"
    :sea_level = "sea_level"
    :grnd_level = "grnd_level"
    :humidity = "humidity"
    :temp_kf = "temp_kf"
    v-show ="isModalVisible"
    @close="closeModal"
  />
</div>
</template>



<script>

import axios from "axios";
<style>@import './css/style.css';</style>
import 'bootstrap-vue/dist/bootstrap-vue.css';
import 'bootstrap/dist/css/bootstrap.css';
import cityDetails from './components/cityDetails.vue';


export default {
    components: {
      cityDetails,
  },
  data(){
    return {
      city:'',
      cityList:[],
      isModalVisible: false,
      cityTitle: ''
    }

  },

  created (){
  },

  methods: {
    
    showModal() {
        this.isModalVisible = true;
    },
    closeModal() {
        this.isModalVisible = false;
    },

    emptyList(){
      this.cityList = [];
    },

    searchCity(){
      this.apiCallList('http://api.openweathermap.org/geo/1.0/direct?q='+ this.city + '&limit=10&appid=8a81160d794a7c7ff46372e14aef240f');

    },

    clickCity(city){
      this.apiCallCity('http://api.openweathermap.org/data/2.5/forecast?lat='+ city.lat +'&lon='+ city.lon +'&appid=8a81160d794a7c7ff46372e14aef240f', city.name );

    },


    getcityList(results){
      this.cityList = results;
    },


    apiCallCity(link, city_name) {
      try {
        axios.get(link)
        .then(function (response) {

          this.tmp = response.data.list[0].main.temp;
          this.feels_like = response.data.list[0].main.feels_like; 
          this.temp_min = response.data.list[0].main.temp_min; 
          this.temp_max = response.data.list[0].main.temp_max;
          this.pressure = response.data.list[0].main.pressure;
          this.sea_level = response.data.list[0].main.sea_level;
          this.grnd_level = response.data.list[0].main.grnd_level;
          this.humidity = response.data.list[0].main.humidity;
          this.temp_kf = response.data.list[0].main.temp_kf;                 


          this.weatherDetails = response.data.list[1].weather[0].main;
          this.weatherDetailsIcon = "http://openweathermap.org/img/w/" + response.data.list[1].weather[0].icon + ".png";
          
          this.cityTitle = city_name;
          this.showModal();

        }.bind(this));
      }
      catch (err) {
        console.log("error: " + err);
      }
    },

    apiCallList(link) {
      const result = [];
      try {
        axios.get(link)
        .then(function (response) {
          for (var i=0;i < response.data.length; i++){
            result.push({name: response.data[i].name,country: response.data[i].country, state: response.data[i].state, lat: response.data[i].lat, lon: response.data[i].lon } );
          }
          this.getcityList(result);
        }.bind(this));
      }
      catch (err) {
        console.log("error: " + err);
      }
    },


  }

}
</script>

<style>@import './css/style.css';</style>


