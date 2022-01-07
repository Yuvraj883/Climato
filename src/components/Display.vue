<template>
  <div class="container">
    <input  @keyup.enter="apiCall" placeholder="Search a city" v-model="city" />
    <button  @click="apiCall">Search</button>

    <div class="display" v-if = "typeof weather.main != 'undefined' ">
      <h2>{{weather.name}}</h2>
      <p>Temperature:{{weather.main.temp}}</p>
      <p>Humidity: {{weather.main.humidity}}</p>
      <p>Wind Speed:{{weather.wind.speed}}</p>
      <p>Description:{{weather.description}}</p>
    </div>
  </div>
</template>
<script>
    import axios from 'axios'

export default{
    name: 'Display',
    data(){
        return{
        city:null,
        apikey:"b99b652d448e47e5a48a226c5ed84910",
        url:null,
        weather:{}
        }
    },
    methods:{
        urlConstructor(){
            
           return this.url="api.openweathermap.org/data/2.5/weather?q="+this.city+"&appid="+this.apikey;
        },
        apiCall(){
            console.log("Api Call initiated ", this.city);
            
    axios.get("https://api.openweathermap.org/data/2.5/find?q=" +this.city+ "&units=metric&appid=b99b652d448e47e5a48a226c5ed84910")
    .then(res=>{
        return res.json;
    })
    .then(this.setResult)
    .catch(error=>{
        console.log("error:" ,error)
    });
        },
        setResult(result){
            this.weather= result;
        }
    },

    props:{
        msg:{
            type:String, 
            default: 'Passed a prop'
        }
    }
}
</script>
<style scoped>
.container {
  height: 30vh;
  min-width: 300px;
  max-width: 700px;
  background-color: black;
  margin: auto;
  padding: 2rem;
  color: white;
  font-weight: bold;
}
input {
  border-radius: 0.5em;
  height: 5vh;
  width: 70%;
}
.display {
  margin-top: 2rem;
  text-align: left;
  margin-left: 15%;
}
</style>

