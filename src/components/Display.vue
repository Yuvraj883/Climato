        <template>
  <div class="container">
    <input @keyup.enter="apiCall" placeholder="Search a city" v-model="city" />
    <button @click="apiCall"><i class="fa fa-search"></i></button>

  
    <div>
      <h2>
        {{ isSet ? weather.list[0].name + ", " : ""
        }}{{ isSet ? weather.list[0].sys.country : "" }}
      </h2>
    </div>

    <div style="display: none" id="infoDiv">
      <p class="temp">
        {{ isSet ? Math.round(weather.list[0].main.temp) + "°C" : "No temp" }}
      </p>

     <img :src="getImgURL()" alt="Icon could not be loaded" />

      <p>
        <b>{{ isSet ? weather.list[0].weather[0].main : "" }}</b>
      </p>

      <p>
        Humidity:
        {{ isSet ? weather.list[0].main.humidity + "%" : "No humidity" }}
      </p>
      <p>
        Wind Speed:{{
          isSet ? weather.list[0].wind.speed + "Km/h" : "No Speed"
        }}
      </p>
    </div>
    <div v-if= "showTime" class="dt">
      <h3>{{ printTime }}</h3>
      <p>{{ printDate }}</p>
    </div>

    <!--<div class="display" v-if = "typeof isSet != false ">-->

    <!--</div>-->
  </div>
  
  <footer>
      <p>Copyright&#169; 2022  </p>
  </footer>
</template>
    <script>
//import axios from 'axios'

export default {
  name: "Display",
  data() {
    return {
      showTime: true,
      time: "",
      date: "Date will be displayed here",
      city:"",
      apikey: "b99b652d448e47e5a48a226c5ed84910",
      url: null,
      weather: {},
      isSet: false,
      icon: "/",
    };
  },

  computed: {
    printDate() {
      return new Date().toLocaleDateString();
    },
    printTime() {
      return new Date().toLocaleTimeString();
    },
  },

  methods: {
    getImgURL() {
      return this.icon;
    },
    urlConstructor() {
      return (this.url =
        "api.openweathermap.org/data/2.5/weather?q=" +
        this.city +
        "&appid=" +
        this.apikey);
    },

    apiCall() {
      if (this.city === "" || this.city===null || this.city===undefined|| this.city.length<=0||typeof this.city==="undefined") {
        alert("Enter a city name");
      } else {
        this.showTime = false;

    //    console.log("Api Call initiated ", this.city);
        /*const data1 = await fetch("https://api.openweathermap.org/data/2.5/find?q=delhi&units=metric&appid=b99b652d448e47e5a48a226c5ed84910"); 
                const data2 = await data1.json(); */
        fetch(
          "https://api.openweathermap.org/data/2.5/find?q=" +
            this.city +
            "&units=metric&appid=b99b652d448e47e5a48a226c5ed84910"
        )
          .then((value) => {
            return value.json();
          })
          .then((value) => {
            this.weather = value;
            this.isSet = true;
          });
        this.isSet = true;
       document.getElementById("infoDiv").style.display = "block";
        this.icon =
         require("https://openweathermap.org/img/wn/" +
          this.weather.list[0].Weather[0].icon +
          ".png");
        this.icon = true;
        //this.weather = data2;
        //console.log(data2);
        this.$emit("setImage", this.city);

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
  },
  created() {
    //     axios.get("https://api.openweathermap.org/data/2.5/find?q="+this.city+"&units=metric&appid=b99b652d448e47e5a48a226c5ed84910")
    //     .then((value) => {return value.json()})
    //         .then((value) => {this.weather = value; this.isSet = true; })
    //         .catch(error=>console.log(error));
    //          document.getElementById('infoDiv').style.display = "block";
   //  this.apiCall();
   // this.city='Mumbai';
  },

  props: {
    msg: {
      type: String,
      default: "Passed a prop",
    },
  }
  // mounted: function () {
  
  //   this.apiCall();
  // },
};
</script>
    <style scoped>
.container {
  min-height: 20vh;
  min-width: 300px;
  max-width: 700px;
  background: black;
  margin: auto;
  padding: 1rem;
  color: whitesmoke;
  font-weight: bold;
}
input {
  border-radius: 0.5em;
  height: 5vh;
  width: 70%;
}
.dt {
  /* position: fixed;
  right:0px bottom 0px;
  padding-left:5rem;
  padding-bottom: 2rem;
  display: block;
  margin:1rem;
 */
 margin:auto;
}

.dt h3 {
  margin: 0px;
}
.dt p {
  margin: 0px;
}
.display {
  margin-top: 2rem;
  text-align: left;
  margin-left: 15%;
}
.temp {
  font-size: 3rem;
  text-shadow: 0.5rem;
  font-weight: 900;
  padding-bottom: none;
  margin: 0;
}
footer{
    background: black;
    color:red;
    position : absolute;
    bottom:0;
    width:100%;
}
</style>
    <style scoped >
@import url("https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css");
.fa-search {
  margin-top: inherit;
  font-size: 1.6rem;
  padding: none;
}
</style>

