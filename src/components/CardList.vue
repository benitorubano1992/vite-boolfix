<script>
import { store } from "../store";
import AppCard from "./AppCard.vue";
export default {
    name: "CardList",
    components: {
        AppCard
    },
    props: {
        message: String,
        list: Array,
    },
    data() {
        return {
            store,
            currentItem: 0,
        }
    },
    methods: {
        getProperty(object) {
            return Object.keys(object);
        }
    }

}


</script>
<template>



    <p>{{ message }}</p>
    <div class="prova">
        <p v-for="key in getProperty(list[currentItem])">{{ key }}</p>
    </div>
    <div class="flex-container">
        <AppCard v-for="film in list" :title="film.title" :Otitle="film.original_title" :Lingua="film.original_language"
            :Overview="film.overview" />
    </div>
</template>
<style scoped>
.flex-container {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
}

.prova {
    background-color: red;
    color: white;
}
</style>