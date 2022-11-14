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
      store
    }
  },
  created: function () {
    /*axios.get(`${this.store.apiUrlMovie}?api_key=${this.store.key}&query=lord`)
      .then(resp => console.log(resp.data))
    */
  },
  methods: {
    printUpdateApi: function () {
      const newApiFilm = `${this.store.apiUrlMovie}?api_key=${this.store.key}&query=${this.store.inputKey}`
      const newApiTV = `${this.store.apiUrlSeries}?api_key=${this.store.key}&query=${this.store.inputKey}`;
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

      this.getApi(newApiFilm).then(data => {
        this.store.loading = true;
        if (data.results) {
          this.store.listFilm = data.results;
        }
        else {
          this.store.listFilm = [];
        }
        console.log(this.store.listFilm)
      })




      this.getApi(newApiTV).then(data => {
        if (data.results) {
          this.store.listSeries = data.results;
        }
        else
          this.store.listSeries = [];
        console.log("lista serie:", this.store.listSeries);
      })




    },
    getApi: async function (url) {
      const response = await fetch(url);
      const data = await response.json();
      return data;
    }

  }

}




</script>
<template>
  <AppHeader @clickInput="printUpdateApi" />
  <main>
    <div class="loading" v-if="!store.loading">Ricerca il tuo primo Film</div>

    <div class="container" v-if="(store.listFilm.length > 0 || store.listSeries.length > 0) && store.loading">
      <CardList message="Lista Film" :list="store.listFilm" />
      <CardList message="Lista Serie" :list="store.listSeries" />

    </div>


  </main>

</template>
<style >
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: aqua;

}

h1 {
  color: red;
}

.container {
  width: 90%;
  margin: 0 auto;
}
</style>
