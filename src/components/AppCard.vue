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
        cardId: Number,
        type: String,
        generi: Array,
    },
    data() {
        return {
            store,
            hasCardHover: false,
            isTrueGenere: null,
            listActor: [],
        }
    },
    methods: {
        updatehasCardHover: function () {
            let url = "";
            if (this.type === "tv")
                url = `https://api.themoviedb.org/3/movie/${this.cardId}/credits?`;
            else
                url = `https://api.themoviedb.org/3/tv/${this.cardId}/aggregate_credits?`;

            console.log(this.cardId)
            console.log(this.type);


            fetch(`${url}api_key=${this.store.key}`)
                .then(resp => resp.json())
                .then(data => {
                    this.listActor = data.cast.filter(actor => actor.order < 5);
                    console.log({ cast: this.listActor });
                    this.hasCardHover = true;
                    if (this.type !== "tv")
                        console.log(this.listActor[0]);
                })
                .catch(error => {
                    this.hasCardHover = true;
                })



        },
        resethasCardHover: function () {
            this.hasCardHover = false;
        },
        getStarsNumber: function () {
            if (votes)
                return Math.ceil(votes / 2);
        },
        getImagePath: function (url) {
            return new URL(url, import.meta.url).href;
        },
        getGeneri: function (array) {
            const listGenre = [];
            if (this.type === "tv")
                this.generi.forEach(genereNum => {
                    for (let genere of this.store.listTvGen) {
                        if (genere.id === genereNum)
                            listGenre.push(genere.name)
                    }
                })
            else {
                this.generi.forEach(genereNum => {
                    for (let genere of this.store.listSerieGen) {
                        if (genere.id === genereNum)
                            listGenre.push(genere.name)
                    }
                })
            }

            return listGenre;
        }

    },



    computed: {
        starsNumber() {
            return Math.ceil(this.votes / 2);
        },
        filterItem() {
            return this.type === "tv" ? (store.filterFilm === 0 || this.generi.includes(store.filterFilm)) : (store.filterSerieTv === 0 || this.generi.includes(store.filterSerieTv))
        }


    }



}






</script>
<template>
    <div class="card" @mouseenter="updatehasCardHover" @mouseleave="resethasCardHover" :data-film="cardId"
        v-show="filterItem">

        <div class=" card-image" v-if="!hasCardHover">
            <img :src="`${this.store.imgPath}/${imageSrc}`" alt="film img" v-if="imageSrc">
            <img src="../assets/icona-nessuna.jpg" alt="immagine rimpitiva" v-else>
        </div>
        <div class="card-text" v-else>
            <p><span>titolo:</span>{{ title }}</p>
            <p><span> Originale:</span>{{ Otitle }}</p>
            <p class="stars" v-if="votes > 0"><span>voto:</span><i class="fa-star" v-for="n in 5"
                    :class="n <= starsNumber ? 'fa-solid' : 'fa-regular'"></i>
            </p>
            <ul>
                <li v-for="(item, index) in getGeneri(generi)">
                    genere{{ index + 1 }}: {{ item }}
                </li>
            </ul>


            <ul class="actor" v-if="listActor.length > 0">
                <li v-for="(actor, index) in listActor" :key="index">{{ type == "tv" ? actor.character :
                        actor.roles[0].character
                }}:
                    interpred by
                    {{ actor.name }} </li>

            </ul>

            <p class="flag-box"><span>Lingua:</span>
                <img class="flag-lingua" :src="getImagePath(`../assets/${Lingua}.png`)" alt="logo bandiera"
                    v-if="Lingua == 'en' || Lingua == 'it'">
                <span v-else>{{ Lingua }}</span>
            </p>
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

ul {
    list-style: none;
}

.card-text {
    padding: 2rem 0.8rem 0 0.8rem;
    height: 100%;
    background-color: black;
    color: white;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
}

.card .flag-lingua {
    width: 50px;
    margin-left: 10px;
}

.flag-box {
    display: flex;
    align-items: center;
}

.card-text p span {
    font-weight: bold;
}

.card-text-description {
    overflow-y: auto;
}
</style>