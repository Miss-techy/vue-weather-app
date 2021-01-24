<template>
<div id="app">

<main>

<div class="search-box">
  <input type="text"
  class="search-bar"
  placeholder="Search..."
  v-model="query"
  v-on:keypress="fetchWeather"  /> <!----when key is pressed implement this method---->






  </div>

<div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
<!----render this if weather is not equal to undefined---->



  <div class="location-box">
<div class="location">{{  weather.name }}, {{ weather.sys.country }} </div>
<div class="date">{{ dateBuilder() }}</div>

</div>  <!----END OF LOCATION-BOX---->

<div class="weather-box">
<div class="temp">{{ Math.round(weather.main.temp) }}
  
  <!----round the temperature to the nearest whole number--->
  
  </div>  
<div class="weather"> {{ weather.weather[0].main }}

  <!----check the actual weather---->
</div>

</div> <!----END OF WEATHER BOX---->

</div> <!----END OF WEATHER WRAP---->

  </main> 

  </div> <!----END OF APP---->
  
</template>

<script>

export default{
  name: 'app',
  
  data() {
    return{
      api_key: 'f61dfd774df2979f488f4cf8897082c5',   //api key from the weather app website
      url_base: 'https://api.openweathermap.org/data/2.5/'  ,     //api base; base of url
      query: '' ,  //to bind the search bar
      weather: {}    //empty data object
    }
  },

  methods: {


  //implement method if the enter key is pressed
    fetchWeather (e) {

      //if the enter key is pressed 

      if(e.key == 'Enter'){

        //fetch is a js api that allows a request to be made

        //using a template string

        

        //weather = to get the current weather  

        //q= stans for query

        // and units = metrics (to use fahrenheit remove this )

        //and pass the api_key

        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)


        //use a callback

        //to get the weather(or response)

        //once the json is returned

        //setResult will be a method implemented below 

        .then(res => {
          return res.json();
        }).then(this.setResults);
      }
    },

    setResults(results) {   //implement the method and pass a paramtert

    //set the weather to rge results
    
    this.weather = results;

    
  },


  dateBuilder() {

    //create a variable and set it to new Date

    //get the months and days

    let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];


    //


    let day = days[d.getDay()];  //get the day

      let date = d.getDate();  //get date 

      let month = months[d.getMonth()]; //get month 

      let year = d.getFullYear();  //get the year -new date + year

      return `${day} ${date} ${month} ${year}`;    //then pull it into a string
  }



}
}


</script>

<style>


*{
  margin:0;
  padding: 0;
  box-sizing: border-box;
}

body{
  font-family:'monserrat', sans-serif;

}

#app{
  background-image:url('./assets/snow.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;

}

main{
  padding:25px;
  min-height: 100vh;
  background-image:linear-gradient(to bottom, rgba(0,0,0,0.25), rgba(0,0,0,0.75) )
}

.search-box{
  width:100%;
  margin-bottom: 30px;
}

.search-box .search-bar{
  display:block;
  width:100%;
  padding:15px; 
  color: #313131;

  appearance: none;
  border: none;
  outline: none;
  background:none;

  background-color: rgba(255, 255, 255, 0.5);

  border-radius: 8px 16px 0px 16px;
  transition: 0.4s;
  
}




.search-box .search-bar:focus{
  box-shadow: 0px 0px 16px;
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0 16px 0;
}


.location-box .location{
  color: white;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-box .date{
  color: white;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;

}

.weather-box{
  text-align: center;
}


.weather-box .temp{
  display: inline-block;
  padding:10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px ;
  margin: 30px 0px;

  box-shadow: 3px 6px rgba(0, 0, 0, 0.5);

}



.weather-box .weather{
  color: white;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0,0,0,0.25);
}
















</style>
