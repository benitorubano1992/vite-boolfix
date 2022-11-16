<script>
import { store } from "../store";
export default {
    name: "AppHeader",
    data() {
        return {
            store,
            selectVal: "",

        }
    },
    methods: {
        printVal: function (valore) {
            console.log(valore);
        },
        filterFilm: function () {
            console.log(this.selectVal, typeof (this.selectVal));
        }
    }


}
</script>
<template>
    <header>
        <div class="choice">
            <h1>Boolfix</h1>
            <div>
                <label class="selectSerie" for="serie">Genere Serie</label>
                <select name="serie" v-model="store.filterSerieTv">
                    <option v-for="genere in store.listSerieGen" :value="genere.id">{{ genere.name }}</option>

                </select>
            </div>
            <div>
                <label class="selectFilm" for="film">Genre Film</label>
                <select name="fims" id="films" v-model="store.filterFilm">
                    <option v-for="genere in store.listTvGen" :value="genere.id">{{ genere.name }}</option>

                </select>
            </div>
        </div>
        <div class="input-box">


            <label for="input-text"></label>
            <input type="text" id="input-text" name="input-text" v-model="store.inputKey"
                placeholder="Cerca il tuo film preferito">
            <button @click="$emit('clickInput')">Submit</button>
        </div>

    </header>
</template>
<style scoped>
header {
    display: flex;
    justify-content: space-between;
    background-color: black;
    align-items: center;
    padding: 15px 10px;
    height: 55px;
}

.choice {
    display: flex;
}

h1 {
    color: red;
    text-transform: uppercase;
    margin-right: 1rem;
}

.selectFilm,
.selectSerie {
    display: block;
    color: white;
}

label {
    display: none;
}

input,
button {
    all: unset;
    padding: 4px 14px;
    border-radius: 0px;
    background-color: white;
    color: black;

}

input {
    font-size: 1rem;
    width: 170px;
}

button {
    background-color: red;
    color: white;
}
</style>