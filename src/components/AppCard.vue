<script>
import { store } from "../store";
export default {
    name: "AppCard",
    props: {
        title: String,
        Otitle: String,
        Lingua: String,
        Overview: String,
        classType: String,
        imageSrc: String,
        votes: Number,
    }
    , data() {
        return {
            store,
            hasCardHover: false
        }
    },
    methods: {
        updatehasCardHover: function () {
            this.hasCardHover = true;
        },
        resethasCardHover: function () {
            this.hasCardHover = false;
        },
        getStarsNumber: function () {
            if (votes)
                return Math.ceil(votes / 2);
        }



    }






}

</script>
<template>
    <div class="card" :class="classType" v-if="classType" @mouseover="updatehasCardHover()"
        @mouseleave="resethasCardHover">
        <div class=" card-image" v-if="!hasCardHover">
            <img :src="`${this.store.imgPath}/${imageSrc}`" alt="film img">
        </div>
        <div class="card-text" v-else>
            <p><span>titolo:</span>{{ title }}</p>
            <p><span> Originale:</span>{{ Otitle }}</p>
            <p class="stars" v-if="votes > 0"><span>voto:</span><span v-for="n in Math.ceil(votes / 2)">⭐</span>
            </p>
            <p><span>Lingua:</span>{{ Lingua }}</p>
            <p class="card-text-description"><span>Overview:</span>{{ Overview }}</p>
        </div>
    </div>
</template>
<style scoped>
.card {
    width: calc(100% / 3 - 30px);
    text-align: center;
    background-color: blue;
    color: white;
    border: 1px solid red;
    margin-bottom: 20px;
    height: 450px;
    cursor: pointer;
}



.card-image {
    height: 100%;
}

.card img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
    object-position: center;
}

.card.tv {
    background-color: blue;
}

.card.serie {
    background-color: green;
}

.card-text {
    padding: 2rem 0.8rem 0 0.8rem;
    height: 100%;
    background-color: black;
    color: white;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.card-text p span {
    font-weight: bold;
}

.card-text-description {
    overflow-y: auto;
}
</style>