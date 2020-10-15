<template>
<div class="container">
    <h1 class="my-4">App météo avec Vue.js</h1>
    <div class="form-group">
        <label for="position">Entrez le nom de la ville</label>
        <input id="position" class="form-control" type="text" v-model="requete" @keypress.enter="goMeteo">
    </div>
    <div v-if="temps" class="w75 m-auto">
        <h3 class="text-center mb-3">Position: {{temps.name}}</h3>
        <div class="card text-center p-5">
            <p class="text-affichage">
                Temperature : {{temps.main.temp.toFixed()}}</p>
            <p class="text-affichage">
                Temps : {{temps.weather[0].description}}</p>
        </div>
    </div>
</div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'meteo',
    mixins: [],
    components: {},
    data() {
        return {
            requete: '',
            temps: undefined,
            api_code: 'f7d02677fa27099d285c9f7d60f2986b',
            url_recherche: 'https://api.openweathermap.org/data/2.5/weather?'
        };
    },
    model: {},
    props: {},
    methods: {
        goMeteo: function () {

            axios
                .get(`${this.url_recherche}q=${this.requete}&units=metric&APPID=${this.api_code}&lang=fr`)
                .then(reponse => {
                    this.temps = reponse.data;
                    console.log(this.temps)

                })
            this.requete = ''

        }
    },
    computed: {},
    watch: {},
}
</script>

<style  scoped>
</style>
