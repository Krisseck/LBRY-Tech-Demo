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
    </v-container>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
    }
  },
  name: 'App'
}
</script>

<style lang="scss">

@import 'scss/variables';

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