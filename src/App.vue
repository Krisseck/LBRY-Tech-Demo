<template>
  <v-app>
    <v-container grid-list-md text-xs-center>
      <v-layout row wrap id="navigation">
        <v-flex xs4>
          <router-link to="/step-1">
            <v-btn color="success" fab>1</v-btn>
            Resolve a claim
          </router-link>
        </v-flex>
        <v-flex xs4>
          <router-link to="/step-2">
            <v-btn color="success" fab>2</v-btn>
            Download a stream
          </router-link>
        </v-flex>
        <v-flex xs4>
          <router-link to="/step-3">
            <v-btn color="success" fab>3</v-btn>
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

#navigation {
  a {
    text-decoration: none;
  }
}

</style>