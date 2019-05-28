<template>
    <div>
        <div class="container">
            <div class="row">
                <div class="col-sm-6 offset-sm-3">
<div class="wrap">
    <img src="../assets/rain.png" style="    
    width: 70px;
    margin-bottom: 20px;
    margin-top: 15px;
    margin-left: 10px;"/>
                       <select class="form-control weather-select" v-model="selectedCity">
            <option disabled selected value="">Please select city </option>
            <option value="51.5074,0.1278">London</option>
            <option value="35.6762,139.6503">Tokyo</option>
            <option value="40.7128,74.0060">New York</option>
            <option value="25.2048,55.2708">Dubai</option>
        </select>
             <div style="margin-top: 15px;" v-if="temperature"><span class="cc">temperature</span> <div class="temp">{{ temperature }} <sup class="sup">°F</sup></div></div>
             <div v-if="summary"> <div class="c-font"> <img class="qq" src="../assets/111.png"/>{{ summary }}</div> </div>
</div>
                </div>
            </div>
         
        </div>


    </div>
</template>

<script>
import axios from 'axios';

export default {
    name:'forecast',
    data() {
        return {
            selectedCity: '',
            temperature: null,
            summary: null,
        }
    },
    watch: {
        selectedCity: async function (city) {
            var coordinates = city.split(',');
            var url = 'https://cors-anywhere.herokuapp.com/'+'https://api.darksky.net/forecast/d6f6dd486e6795355ef8827e6e8c6b9c/'+coordinates[0]+','+ coordinates[1];
            await axios
            .get(url)
            .then(response => {
                var temperature = response.data.currently.temperature;
                this.temperature = temperature;
                var summary = response.data.currently.summary;
                this.summary = summary;
            })
            .finally() 
        }
    },

}
</script>


<style>

@import url('https://fonts.googleapis.com/css?family=Poppins:100,100i,200,200i,300,300i,400,400i,500,500i,600,600i,700&display=swap');

body {    
    height: -webkit-fill-available;
    background: url(../assets/Sky-Wallpapers.jpg);
    font-family: 'Poppins', sans-serif;}
.wrap {
    padding: 20px;
    background: #fff9;
    border-radius: 4px;
    text-align: left;
        box-shadow: 1px 3px 7px 0px #ababab;}

.weather-select {
    -webkit-appearance: none;
    border: 1px solid #cecece !important;
    border-radius: 2px !important;
    background: url(https://cdn.iconscout.com/icon/free/png-256/chevron-down-457657.png);
    background-size: 14px;
    background-repeat: no-repeat;
    background-position: center;
    background-position-x: 98%;}

.c-font {font-style: italic;
    display: inline-block;
    border: 1px solid #a5a2a2;
    padding: 5px 20px;
    border-radius: 32px;
    font-size: 13px;
    background: #fff;}

 .temp { font-size: 75px;}   

    .qq {    width: 16px;
    opacity: 0.5;
    margin-right: 8px;}

.cc {font-size: 24px;
    font-weight: 100;
    line-height: 0px;}

    .sup {    font-size: 30px;
    top: -1.5em;
    right: 10px;}
</style>
