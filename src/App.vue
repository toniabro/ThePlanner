<template>
  <v-app>
    <v-navigation-drawer v-model="drawer" app>
      <v-list nav dense>
        <v-list-item-group active-class="primary--text">
          <v-list-item @click="routeTo('/')">
            <v-list-item-icon>
              <v-icon>mdi-home</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Home</v-list-item-title>
          </v-list-item>
          <v-list-item v-on:click="routeTo('/todo')">
            <v-list-item-icon>
              <v-icon>mdi-checkbox-marked-outline</v-icon>
            </v-list-item-icon>
            <v-list-item-title>The Todo</v-list-item-title>
          </v-list-item>
          <v-list-item v-on:click="routeTo('/workout')">
            <v-list-item-icon>
              <v-icon>mdi-run</v-icon>
            </v-list-item-icon>
            <v-list-item-title>The Workout Journal</v-list-item-title>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar color="#ccffff" app>
      <v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>
    </v-app-bar>

    <!-- Sizes your content based upon application components -->
    <v-main>
      <!-- Provides the application the proper gutter -->
      <v-container fluid>
        <!-- If using vue-router -->
        <router-view></router-view>
      </v-container>
    </v-main>

    <v-footer app>
      <!-- -->
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'App',

  data: () => ({
    drawer: false
  }),

  methods: {
    routeTo(newPath) {
      this.$router.push({ path: newPath })
    }
  }
}
</script>

<style>
#app {
  font-family: Helvetica;
  background-color: white;
}
</style>
