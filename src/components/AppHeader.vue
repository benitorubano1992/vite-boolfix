<script>
import { store } from "../store";
export default {
    name: "AppHeader",
    data() {
        return {
            store
        }
    }
}
</script>
<template>
    <header>
        <h1>Boolfix</h1>
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
}

h1 {
    color: red;
    text-transform: uppercase;
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