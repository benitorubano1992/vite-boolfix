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
      const newApi = `${this.store.apiUrlMovie}?api_key=${this.store.key}&query=${this.store.inputKey}`

      /*axios.get(newApi).then(resp => {
        console.log(resp.data);
        this.store.listFilm = resp.data;
      })*/

      this.getApi(newApi).then(data => {

        this.store.listFilm = data.results;
        console.log(this.store.listFilm);
        for (let i = 0; i < this.store.listFilm.length; i++) {
          console.log(this.store.listFilm[i]);
        }
      });

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
    <div class="container">
      <CardList message="Lista Film" :list="store.listFilm" />
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
</style>
