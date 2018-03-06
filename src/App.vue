<template>
  <v-app>
    <v-container grid-list-md text-xs-center>
      <v-layout row wrap id="navigation">
        <v-flex xs4>
          <router-link exact to="/">
            <v-btn color="grey" fab>1</v-btn>
            Resolve a claim
          </router-link>
        </v-flex>
        <v-flex xs4>
          <router-link to="/step-2">
            <v-btn color="grey" fab>2</v-btn>
            Publish content
          </router-link>
        </v-flex>
        <v-flex xs4>
          <router-link to="/step-3">
            <v-btn color="grey" fab>3</v-btn>
            Support with LBC
          </router-link>
        </v-flex>
      </v-layout>
      <router-view/>
      <v-dialog v-model="uploadDialog" hide-overlay persistent width="30rem">
        <v-card>
          <template v-if="confirmed">
            <v-card-title class="headline">Your image has been published!</v-card-title>
            <v-card-text><a v-bind:href="'https://explorer.lbry.io/tx/' + txhash" target="_blank">Check out your content on the LBRY blockchain explorer</a></v-card-text>
            <v-card-actions>
              <v-btn v-on:click="uploadDialog = false" flat>Dismiss this dialog</v-btn>
            </v-card-actions>
          </template>
          <template v-else>
            <v-card-title class="headline"><v-progress-circular indeterminate color="primary"></v-progress-circular>&nbsp;Waiting for confirmations...</v-card-title>
            <v-card-text>Your image was uploaded to the LBRY network but we are currently waiting for the first confirmation. This should take just a few minutes. In the mean time, go ahead and try the other steps!</v-card-text>
          </template>
        </v-card>
      </v-dialog>
    </v-container>
  </v-app>
</template>

<script>

import EventBus from './event-bus';

export default {
  data () {
    return {
      uploadDialog: false,
      txhash: '',
      confirmed: false
    }
  },
  watch: {
    uploadDialog: function() {
      var component = this;
      if(this.uploadDialog) {
        // Simulate confirmation
        setTimeout(function() {
          component.confirmed = true;
        }, 10000)
      }
    }
  },
  created () {
    var component = this;
    EventBus.$on('file-uploaded', function(txhash) {
      component.txhash = txhash;
      component.uploadDialog = true;
    });
  },
  name: 'App'
}
</script>

<style lang="scss">

@import 'scss/variables';

@import '../node_modules/highlight.js/styles/monokai-sublime';

pre {
  text-align: left;
  overflow-x: auto;
}

.dialog__content {
  align-items: flex-end !important;
  justify-content: right !important;
}

#app {
  background: lighten(desaturate($primary-color,30%), 50%);
  color: $text-color;
}

#navigation {
  a {
    text-decoration: none;
    color: $text-color;
  }
  .router-link-active {
    font-weight: bold;
    .btn {
      background: $primary-color !important;
      color: white !important;
    }
  }
}

</style>