<script>
export default {
    name: "AppCard",
    props: {
        title: String,
        Otitle: String,
        Lingua: String,
        Overview: String,
    }
    , data() {
        return {

        }
    }
}

</script>
<template>
    <div class="card">
        <p>titolo:{{ title }}</p>
        <p>titolo Originale:{{ Otitle }}</p>
        <p>Lingua:{{ Lingua }}</p>
        <p>Overview:{{ Overview }}</p>
    </div>
</template>
<style scoped>
.card {
    width: calc(100% / 3 - 10px);
    text-align: center;
    background-color: blue;
    color: white;
    border: 1px solid red;
    margin-bottom: 20px;
}
</style>