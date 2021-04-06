<template>
  <div class="container">
    <div class="content">
      <div class="search_box" v-if="always">
        <h3>Rechercher une ville :</h3>
        <input type="text" name="query" v-model="query" @keypress="fetchWeather">
      </div>
      <!-- ===== WEATHER IN THE CURRENT CITY ===== -->
      <div class="weather" v-if="seen">
        <div class="city_info">
          <div class="city_name">
            <h1>{{ weather.name }}, {{ weather.sys.country }}</h1>
            <p>{{ dateBuilder() }}</p>
          </div>
          <div class="city_coor">
            <p><span>Longitude :</span> {{ weather.coord.lon }} </p>
            <p><span>Latitude :</span> {{ weather.coord.lat }}</p>
          </div>
          <div class="city_sun">
            <p class="sunrise"><span>Levé du soleil :</span> {{ timeConvert(weather.sys.sunrise) }} </p>
            <p class="sunset"><span>Couché du soleil :</span> {{ timeConvert(weather.sys.sunset) }} </p>
          </div>
        </div>
        <div class="city_weather">
          <div class="city_weather_temp">
            <div class="temp">
              <p class="min">Min <br>{{ Math.round(weather.main.temp_min) }}°C</p>
            <p class="temp">{{ Math.round(weather.main.temp) }}°C</p>
              <p class="max">Max <br> {{ Math.round(weather.main.temp_max) }}°C</p>
            </div>
            <p class="mom">{{ weather.weather[0].description }}</p>
          </div>
          <div class="weather_info">
            <div class="wind">
              <p><span>Vitesse du vent</span> <br> {{ weather.wind.speed }} m/s</p>
            </div>
            <div class="humidity">
              <p><span>Humidité</span> <br> {{ weather.main.humidity }}%</p>
            </div>
            <div class="precipitation">
              <p><span>Visibilité</span> <br> {{ weather.visibility / 1000 }} km</p>
            </div>
          </div>
        </div>
      </div>
      <!-- ===== WEATHER IN CITY USER SEARCH ===== -->
      <div class="weather" v-if="seen2">
        <div class="city_info">
          <div class="city_name">
            <h1>{{ weather.name }}, {{ weather.sys.country }}</h1>
            <p>{{ dateBuilder() }}</p>
          </div>
          <div class="city_coor">
            <p><span>Longitude :</span> {{ weather.coord.lon }} </p>
            <p><span>Latitude :</span> {{ weather.coord.lat }}</p>
          </div>
          <div class="city_sun">
            <p class="sunrise"><span>Levé du soleil :</span> {{ timeConvert(weather.sys.sunrise) }} </p>
            <p class="sunset"><span>Couché du soleil :</span> {{ timeConvert(weather.sys.sunset) }} </p>
          </div>
        </div>
        <div class="city_weather">
          <div class="city_weather_temp">
            <div class="temp">
              <p class="min">Min <br>{{ Math.round(weather.main.temp_min) }}°C</p>
            <p class="temp">{{ Math.round(weather.main.temp) }}°C</p>
              <p class="max">Max <br> {{ Math.round(weather.main.temp_max) }}°C</p>
            </div>
            <p class="mom">{{ weather.weather[0].description }}</p>
          </div>
          <div class="weather_info">
            <div class="wind">
              <p><span>Vitesse du vent</span> <br> {{ weather.wind.speed }} m/s</p>
            </div>
            <div class="humidity">
              <p><span>Humidité</span> <br> {{ weather.main.humidity }}%</p>
            </div>
            <div class="precipitation">
              <p><span>Visibilité</span> <br> {{ weather.visibility / 1000 }} km</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      always: true,
      seen2: false,
      seen: false,
      api_key: '4904538d41bfc39b8c10759f5776286c',
      base_url: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  mounted () {
    if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition((position) => {
        fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${position.coords.latitude}&lon=${position.coords.longitude}&units=metric&lang=fr&appid=4904538d41bfc39b8c10759f5776286c`)
          .then(res => {
            return res.json()
          })
          .then((results) => {
            this.weather = results
            console.log("weather ", this.weather)
            this.seen = true
          })
    })
    } else {
      console.log("not geolocation")
    }
  },
  methods: {
    fetchWeather (e) {
      if (e.key == 'Enter') {
        fetch(`${this.base_url}weather?q=${this.query}&units=metric&lang=fr&APPID=${this.api_key}`)
         .then(res => {
           return res.json()
         })
         .then(this.setResults)
      }
    },
    setResults (results) {
      this.weather = results
      console.log("weather ", this.weather)
      this.seen = false
      this.seen2 = true
    },
    timeConvert (unix) {
      let a = new Date(unix * 1000)
      let hours = a.getHours()
      let minutes = a.getMinutes()
      return `${hours}h${minutes}`
    },
    dateBuilder () {
      let d = new Date()
      let months = ["Janvier", "Février", "Mars", "Avril",
      "Mai", "Juin", "Juillet", "Aout", "Septembre", "Octobre",
      "Novembre", "Décembre"]

      let days = ["Dimanche", "Lundi", "Mardi", "Mercredi",
      "Jeudi", "Vendredi", "Samedi"]

      let day = days[d.getDay()]
      let date = d.getDate()
      let month = months[d.getMonth()]
      let year = d.getFullYear()

      return `${day} ${date} ${month} ${year}`
    }
  }
}
</script>

<style>
.search_box {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 30px;
}

.search_box h3 {
  margin-right: 20px;
  text-transform: uppercase;
}

.search_box input {
  width: 270px;
  height: 50px;
  border: 1px solid black;
  border-radius: 8px;
  padding: 0 10px;
}

.search_box input:focus {
  border: 1px solid black;
  outline: none;
}

.weather {
  display: flex;
  justify-content: space-around;
  margin-top: 90px;
}

.weather .city_info {
  width: 50%;
  border-right: 1px solid rgba(0, 0, 0, 0.274);
}

.weather .city_weather {
  width: 50%;
}

.weather .city_info .city_name h1 {
  font-size: 50px;
  margin-bottom: 15px;
  text-transform: capitalize;
}

.weather .city_info .city_coor {
  display: flex;
  justify-content: space-around;
  margin-top: 40px;
}

.weather .city_info .city_coor span {
  font-weight: 600;
  text-transform: uppercase;
}

.weather .city_info .city_sun {
  margin-top: 55px;
}

.weather .city_info .city_sun .sunrise {
  margin-bottom: 15px;
}

.weather .city_info .city_sun span {
  font-weight: 600;
  text-transform: uppercase;
}




.city_weather .city_weather_temp .temp {
  width: 70%;
  margin: auto;
  display: flex;
  justify-content: space-around;
  align-items: center;
  font-size: 65px;
}

.city_weather .city_weather_temp .temp .max, .min {
  font-size: 20px;
}

.city_weather .city_weather_temp .mom {
  font-size: 25px;
  text-transform: capitalize;
}

.city_weather .weather_info {
  width: 100%;
  margin: auto;
  margin-top: 60px;
  display: flex;
  justify-content: space-around;
}

.city_weather .weather_info span {
  font-size: 21px;
}

.city_weather .weather_info .wind {
  width: 33%;
}

.city_weather .weather_info .humidity {
  width: 33%;
  border-left: 1px solid rgba(0, 0, 0, 0.274);
  border-right: 1px solid rgba(0, 0, 0, 0.274);
}

.city_weather .weather_info .precipitation {
  width: 33%;
}
</style>
