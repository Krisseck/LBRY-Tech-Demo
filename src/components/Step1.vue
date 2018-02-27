<template>
  <v-container fluid>
    <v-layout row wrap>
      <v-flex xs12>
        <h1 class="display-2">Learn the LBRY protocol by examples</h1>
        <p class="subheading">Let's start by getting the associated metadata for <a href="#">a claim</a>.</p>
      </v-flex>
      <v-flex xs10>
        <v-text-field v-model="address" solo dark prefix="lbry://"></v-text-field>
      </v-flex>
      <v-flex xs2>
        <v-btn color="primary" v-on:click="fetchMetadata">Execute</v-btn>
      </v-flex>
      <v-flex xs12 v-if="isLoading">
        <p class="subheading">Loading...</p>
      </v-flex>
      <v-flex xs12 v-if="jsonData">
        <pre v-highlightjs="jsonData" class="json-example"><code class="json"></code></pre>
      </v-flex>
      <template v-if="!isLoading">
        <v-flex xs12>
          <p class="subheading">... or select a live example from below</p>
        </v-flex>
        <v-flex xs3>
          <v-card hover>
            <v-card-media src="static/itsadisaster.jpg" height="200px" v-on:click="chooseClaim('itsadisaster')">
            </v-card-media>
            <v-card-title primary-title v-on:click="chooseClaim('itsadisaster')">
              <div>
                <h3 class="headline mb-0">It's a Disaster</h3>
                <div>Four couples meet for Sunday brunch only to discover they are stuck in a house together as the world may be about to end.</div>
              </div>
            </v-card-title>
          </v-card>
        </v-flex>
        <v-flex xs3>
          <v-card hover>
            <v-card-media src="static/unbubbled.png" height="200px" v-on:click="chooseClaim('unbubbled1-1')">
            </v-card-media>
            <v-card-title primary-title v-on:click="chooseClaim('unbubbled1-1')">
              <div>
                <h3 class="headline mb-0">Unbubbled with Jamie King, Ep1.1 - Bitcoin, Boom or Bust</h3>
                <div>For more of Jamie King and free, uncensored content: stream from the LBRY app directly at lbry://unbubbled1-1 and his STEAL THIS SHOW podcast extras at - lbry://@stealthisshow -\n\nThis is the Pilot episode of Unbubbled, a new show from producer Jamie King (STEAL THIS FILM, STEAL THIS SHOW).</div>
              </div>
            </v-card-title>
          </v-card>
        </v-flex>
        <v-flex xs3>
          <v-card hover>
            <v-card-media src="static/fortnite.jpg" height="200px" v-on:click="chooseClaim('fortnite-top-stream-moments-nickatnyte')">
            </v-card-media>
            <v-card-title primary-title v-on:click="chooseClaim('fortnite-top-stream-moments-nickatnyte')">
              <div>
                <h3 class="headline mb-0">FORTNITE TOP STREAM MOMENTS - Nickatnyte & GamingwithMolt</h3>
                <div>Watch Fortnite live here -- http://bit.ly/nickatnyte2 -- Fortnite Battle Royale Live Stream highlights of the week!</div>
              </div>
            </v-card-title>
          </v-card>
        </v-flex>
        <v-flex xs3>
          <v-card hover>
            <v-card-media src="static/lbrymine.png" height="200px" v-on:click="chooseClaim('six')">
            </v-card-media>
            <v-card-title primary-title v-on:click="chooseClaim('six')">
              <div>
                <h3 class="headline mb-0">LBRY Coin (LBC) GPU Miner for AMD and NVIDIA</h3>
                <div>AMD/NVIDIA LBRY Miners - sgminer/ccmniner\nWith Guides + Pool Configs</div>
              </div>
            </v-card-title>
          </v-card>
        </v-flex>
      </template>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data () {
    return {
      address: 'Claim goes here',
      jsonData: '',
      isLoading: false
    }
  },
  methods: {
    fetchMetadata () {
      var component = this;
      component.jsonData = '';
      component.isLoading = true;
      this.$http.get('http://daemon.lbry.tech/?method=resolve&uri=' + this.address).then(function(response) {
        component.isLoading = false;
        component.jsonData = JSON.stringify(response.body, null, '  ');
      });
    },
    chooseClaim (address) {
      var component = this;
      component.address = address;
      component.fetchMetadata();
    }
  },
  name: 'Step1'
}
</script>

<style lang="scss">

  @import '../../node_modules/highlight.js/styles/monokai-sublime';

  .json-example {
    text-align: left;
    overflow-x: scroll;
  }

</style>