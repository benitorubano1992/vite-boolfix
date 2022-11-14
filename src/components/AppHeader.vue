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
            <input type="text" id="input-text" name="input-text" v-model="store.inputKey">
            <button @click="$emit('clickInput')">Submit</button>

        </div>
    </header>
</template>
<style scoped>

</style>