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
            isTv: false
        }
    },
    methods: {
        getProperty(object) {
            const listProp = Object.keys(object);
            const result = {};
            if (listProp.includes("original_title")) {
                result.title = object.title;
                result.original_title = object.original_title;

                result.class = "tv"
            }
            else if (listProp.includes("name")) {
                result.title = object.name;
                result.original_title = object.original_name;

                result.class = "serie"
            }
            result.original_language = object.original_language;
            result.overview = object.overview;
            result.poster_path = object.poster_path
            result.average = object.vote_average;


            return result;

        }

    }
}

</script>
<template>



    <p>{{ message }}</p>
    <!--<div class="prova" v-if="list.length > 0">
        <p v-for="(value, key) in getProperty(list[currentItem])">{{ key }}:{{ value }}</p>
    </div>
-->
    <div class="flex-container" v-if="list.length > 0">
        <AppCard v-for="film in list" :title="getProperty(film).title" :Otitle="getProperty(film).original_title"
            :Lingua="getProperty(film).original_language" :Overview="getProperty(film).overview"
            :classType="getProperty(film).class" :imageSrc="getProperty(film).poster_path"
            :votes="getProperty(film).average" />
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