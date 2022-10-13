<template>
  <div>
    <v-container>
      <h2>Rechercher une ville</h2>
    </v-container>

    <v-form @submit.prevent="submitting" @keyup.enter="submitting">
      <v-container>
        <v-row>
          <v-col cols="12" md="13">
            <v-text-field
              v-model="countrySend"
              filled
              label="Entrez une ville"
              required
              dense
              :counter="30"
            ></v-text-field>
            <v-flex class="text-center">
              <button
                type="button"
                class="mr-4 btn btn-primary me-2 px-5 text-white my-5"
                @click="submitting"
              >
                Rechercher
              </button>
            </v-flex>
          </v-col>
        </v-row>
      </v-container>
    </v-form>

    <!--Card for Results-->
    <v-card
      v-if="results"
      elevation="100"
      style="background-color: #546e7a"
      class="text-center container"
    >
      <div class="container">
        <div class="row">
          <div class="col-md-4 col-12">
            <h6 class="fw-bold fs-2 mt-5 mt-md-0">Température</h6>
            <hr />
            <div id="name" class="h1 col-12">{{ country.name }}</div>
            <div id="imgdesc" class="col">
              <img :src="country.icone" alt="weather description" />
            </div>

            <div class="container row">
              <div id="degre" class="col-6 h1">{{ country.degre }} °C</div>
              <div id="desciption" class="col-6 mt-2 fs-6">
                {{ country.description }}
              </div>
            </div>
          </div>
          <div class="col-12 col-md-4 mt-5 mt-md-0">
            <h6 class="fw-bold fs-2">Vent et Pression:</h6>
            <hr />
            <span id="wind" class="fs-4 col-12">
              Vent : {{ country.windSpeed }} m/s ({{ country.windDeg }}°)
            </span>
            <br />
            <span id="humidity" class="col-12 fs-4">
              Humidité : {{ country.humidity }} %
            </span>
            <br />
            <span id="Pressure" class="col-12 fs-4">
              Pression : {{ country.pressure }} hPa
            </span>
          </div>
          <div class="col-12 col-md-4">
            <h6 class="fw-bold fs-2 mt-5 mt-md-0">Autre :</h6>
            <hr />
            <span id="maxtemp" class="fs-4 col-12">
              Température Maximale : {{ country.maxTemp }} °C
            </span>
            <br />
            <span id="mintemp" class="col-12 fs-4">
              Température Minimale : {{ country.minTemp }} °C
            </span>
          </div>
        </div>
      </div>
    </v-card>
    <div v-if="!results" id="noresult" class="text-center fs-1">
      <div>No Result</div>
      <div style="height: 30vh"></div>
    </div>
  </div>
</template>

<script>
/* eslint-disable no-console */
export default {
  name: 'IndexPage',
  data() {
    return {
      countrySend: '',
      country: {
        name: '',
        description: '',
        icone: '',
        degre: '',
        windSpeed: '',
        windDeg: '',
        humidity: '',
        pressure: '',
        maxTemp: '',
        minTemp: '',
      },
      results: false,
    }
  },

  methods: {
    submitting() {
      this.$axios
        .get(
          'https://api.openweathermap.org/data/2.5/weather?q=' +
            this.countrySend +
            '&appid=639ba8dcb5869fc1036c52f6d5d04f7f'
        )
        .then((res) => {
          this.results = true
          this.country.name = res.data.name
          this.country.description = res.data.weather[0].description
          this.country.icone =
            'https://openweathermap.org/img/w/' +
            res.data.weather[0].icon +
            '.png'
          this.country.degre = Math.round(res.data.main.temp - 273.15)
          this.country.windSpeed = res.data.wind.speed
          this.country.windDeg = res.data.wind.deg
          this.country.humidity = res.data.main.humidity
          this.country.pressure = res.data.main.pressure
          this.country.maxTemp = Math.round(res.data.main.temp_max - 273.15)
          this.country.minTemp = Math.round(res.data.main.temp_min - 273.15)
        })
        .catch(() => {
          alert('Resultat Introuvable !')
        })
    },
  },
}
</script>
