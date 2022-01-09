    <template>
  <div class="container">
    <input @keyup.enter="apiCall" placeholder="Search a city" v-model="city" />
    <button  @click="apiCall">Search</button>

      <div><h2>{{isSet?weather.list[0].name+", ":""}}{{isSet?weather.list[0].sys.country:""}} </h2> </div>
      
      <div style="display:none;" id="infoDiv">
      <p>Temperature:{{isSet?Math.round(weather.list[0].main.temp)+"°C":"No temp"}}</p>
      <div v-show="icon.active">
      <img src={{icon.link}}>

      </div>
      <p>Humidity: {{isSet?weather.list[0].main.humidity+"%":"No humidity"}}</p>
      <p>Wind Speed:{{isSet?weather.list[0].wind.speed+"Km/h":"No Speed"}}</p>
      <p>Description: {{isSet?weather.list[0].weather[0].main:""}}</p>
      </div>
      

      

    <!--<div class="display" v-if = "typeof isSet != false ">-->

      

    <!--</div>-->

  </div>
</template>
<script>
  //import axios from 'axios'

export default{
    name: 'Display',
    data(){
        return{
        city:'Delhi',
        apikey:"b99b652d448e47e5a48a226c5ed84910",
        url:null,
        weather:{}, 
        isSet: false,
        icon:{
            active:false,
            link:"/"
        }
        }
    },
    created(){
        
    //     axios.get("https://api.openweathermap.org/data/2.5/find?q="+this.city+"&units=metric&appid=b99b652d448e47e5a48a226c5ed84910")
    //     .then((value) => {return value.json()})
    //         .then((value) => {this.weather = value; this.isSet = true; })
    //         .catch(error=>console.log(error));

    //          document.getElementById('infoDiv').style.display = "block";
     },
    methods:{
        urlConstructor(){
            
           return this.url="api.openweathermap.org/data/2.5/weather?q="+this.city+"&appid="+this.apikey;
        },
        apiCall(){
            console.log("Api Call initiated ", this.city);
            /*const data1 = await fetch("https://api.openweathermap.org/data/2.5/find?q=delhi&units=metric&appid=b99b652d448e47e5a48a226c5ed84910"); 
            const data2 = await data1.json(); */
            fetch("https://api.openweathermap.org/data/2.5/find?q="+this.city+"&units=metric&appid=b99b652d448e47e5a48a226c5ed84910")
            .then((value) => {return value.json()})
            .then((value) => {this.weather = value; this.isSet = true; })
            //this.isSet = true; 
            document.getElementById('infoDiv').style.display = "block"; 
            this.icon.link= "https://openweathermap.org/img/wn/"+this.weather.list[0].weather[0].icon +".png";
            this.icon.active=true;
            //this.weather = data2; 
            //console.log(data2);
            
            
          /* fetch ("https://api.openweathermap.org/data/2.5/find?q=delhi&units=metric&appid=b99b652d448e47e5a48a226c5ed84910")
 .then(function responseHandler(response){return response.json()})
 .then (function logJson(json){document.getElementById("temp").innerText=json.list["main"].temp})
 .catch(error=>console.log("Error", error))*/


    // axios.get("https://api.openweathermap.org/data/2.5/find?q=" +this.city+ "&units=metric&appid=b99b652d448e47e5a48a226c5ed84910")
    // .then(res=>{
    //     return res.json;
    // })
    // .then(json=>this.weather=json)
    // .catch(error=>{
    //     console.log("error:" ,error)
    // });
    //     },
    //     setResult(result){
    //         this.weather= result;
    //         console.log(this.weather)
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

