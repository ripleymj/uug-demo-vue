<template>
    <main>
        <div>
            <h1>Latest Earthquake (Outside Harrisonburg)</h1>
            <p class="mag"><span>{{ mag }}</span> magnitude</p>
            <p class="location">{{ location }}</p>
            <p class="time">{{ time }}</p>
            <div class="tux">
              <img src="./tux_mask.svg" alt="Tux, the JMU Unix Users Group penguin mascot.">
            </div>
        </div>
    </main>
</template>

<script>
    import axios from 'axios';

    export default {
        name: "app",
        data() {
            return {
                location: "",
                mag: 0.0,
                time: "",
                local: (location.hostname === "localhost")
            }
        },
        methods: {
            getEarthquake() {
                let self = this;
                let endpoint = (this.local)? 'http://localhost:3000/earthquakes/latest' : '/api/earthquakes/latest';
                axios
                .get(endpoint)
                .then(function(response) {
                    self.location = response.data.properties.place;
                    self.mag = response.data.properties.mag;
                    self.time = new Date(response.data.properties.time).toUTCString();
                })
                .catch(function(err) {
                    console.log(err);
                });

            }
        },
        mounted() {
            this.getEarthquake();
        }
    }
</script>

<style scoped>
    @import url('https://fonts.googleapis.com/css2?family=Raleway:wght@300;400;700&display=swap');
    * {
        font-family: 'Raleway', sans-serif;
    }
    html, body {
        width: 100%;
        min-height: 100%;
    }
    body {
        display: flex;
    }
    main {
        display: flex;
        justify-content: center;
        padding-top: 10vh;
    }
    main p {
        font-size: 16px;
    }
    main .mag > span {
        font-size: 24px;
        font-weight: bold;
    }
    main .tux > img {
      margin-top: 24px;
      width: auto;
      max-height: 160px;
    }
</style>
