<script>
import axios from "axios";
import { store } from "./store";
import AppHeader from "./components/AppHeader.vue";
import CardList from "./components/CardList.vue";
export default {
  components: {
    AppHeader,
    CardList
  },
  data() {
    return {
      store,
      errorFilm: false,
      errorSerie: false,
    }
  },
  created: function () {
    /*axios.get(`${this.store.apiUrlMovie}?api_key=${this.store.key}&query=lord`)
      .then(resp => console.log(resp.data))
    */
    axios.get("https://api.themoviedb.org/3/genre/movie/list?api_key=3741027abeb1eb84221d5dad2eb42849&language=en-US")
      .then(resp => {
        this.store.listTvGen = resp.data.genres;

        console.log(this.store.listTvGen, typeof (this.store.listTvGen));
      })
    axios.get("https://api.themoviedb.org/3/genre/tv/list?api_key=3741027abeb1eb84221d5dad2eb42849&language=en-US")
      .then(resp => {
        this.store.listSerieGen = resp.data.genres;
      })

  },
  computed: {
    getError: function () {

      const result = this.errorFilm && this.errorSerie ? "Non ci sono serieTv e Film con questo Nome" :
        this.errorFilm ? "Non ci sono Film con questo Nome" : "Non ci sono Serie Tv con questo Nome";
      return result;
    }
  },

  methods: {
    printUpdateApi: async function () {
      this.store.filterFilm = 0;
      this.store.filterSerieTv = 0;
      const newApiFilm = `${this.store.apiUrlMovie}?api_key=${this.store.key}&query=${this.store.inputKey}`
      const newApiTV = `${this.store.apiUrlSeries}?api_key=${this.store.key}&query=${this.store.inputKey}`;

      this.getFilmList(newApiFilm);
      this.getSerieList(newApiTV);
      console.log({ FilmError: this.errorFilm })
      console.log({ SerieError: this.errorSerie });


      /*try {
        const response = await this.getApi(newApiFilm);
        console.log(response);
        this.store.listFilm = response.results;
      }
      catch (error) {
        console.log("cè stato un errore");
      }
      finally {
        this.store.loading = true;
      }
      */
      /*axios.get(newApi).then(resp => {
        console.log(resp.data);
        this.store.listFilm = resp.data;
      })*/

      /*const promiseList = [newApiFilm, newApiTV];
      const copyArray = [this.store.listFilm, this.store.listSeries];
      for (let i = 0; i < promiseList.length; i++) {
        fetch(promiseList[i])
          .then(resp => resp.json())
          .then(data => {
            this.store.lists.push(data.results);
            console.log(this.store.lists)
          })

      }
    }
    */


      /*this.getApi(newApiFilm).then(data => {
  
        this.store.listFilm = data.results;
        console.log(this.store.listFilm);
        /*for (let i = 0; i < this.store.listFilm.length; i++) {
          console.log(this.store.listFilm[i]);
        }
       
        
  
  
  
      });
      */



      /*this.getApi(newApiFilm).then(data => {
        this.store.listFilm = data.results;
      }).catch(error => {
        console.log("cè stato un errore nei film")
        this.store.listFilm = [];
        console.log(this.store.listFilm);
      })
        .finally(() => {
          this.store.loading = true;
        })

        */


      /*this.getApi(newApiTV).then(data => {

        this.store.listSeries = data.results;
        console.log({ listaSere: this.store.listSeries })
      }).catch(error => {
        console.log("cè stato un errore nelle serie");
        this.store.listSeries = [];
        console.log(this.store.listSeries)
      })
*/





    },
    getFilmList: function (url) {
      axios.get(url)
        .then(response => {
          this.store.listFilm = response.data.results
          console.log(this.store.listFilm)
          this.errorFilm = false;
        })
        .catch(error => {
          this.errorFilm = true;
          console.log("errore nei film")

        })
        .finally(this.store.loading = true);
    },
    getSerieList: function (url) {
      axios.get(url)
        .then(response => {
          this.store.listSeries = response.data.results
          console.log(this.store.listSeries);
          this.errorSerie = false;
        })
        .catch(error => {
          this.errorSerie = true;
          console.log("errore nelle serie")
        })
    }

  }

}


</script>
<template>
  <AppHeader @clickInput="printUpdateApi" />
  <main>
    <div class="loading" v-if="!store.loading">Ricerca il tuo primo Film</div>
    <div class="error-film" v-if="((errorFilm && errorSerie) || errorFilm)">{{ getError }}</div>
    <div class="container" v-if="store.loading && !errorFilm">
      <CardList message="Lista Film" :list="store.listFilm" />
      <div class="error-serie" v-if="!errorFilm && errorSerie">{{ getError }}</div>
      <CardList message="Lista Serie" :list="store.listSeries" />

    </div>


  </main>

</template>
<style lang="scss" >
@use "./styles/general.scss" as *;

main {
  height: calc(100vh - 55px);
  overflow-y: auto;
}


h1 {
  color: red;
}

.container {
  width: 90%;
  margin: 0 auto;
}
</style>
