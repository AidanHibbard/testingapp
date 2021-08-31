<template>
  <div>
    <v-app-bar
      dark
    >
      <v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>
      <NuxtLink to="/">
        <v-toolbar-title>Testing App</v-toolbar-title>
      </NuxtLink>
    </v-app-bar>

    <v-navigation-drawer
      dark
      v-model="drawer"
      absolute
      temporary
    >
      <v-list
        nav
        dense
      >
        <v-list-item-group
          v-model="group"
          active-class="deep-purple--text text--accent-4"
        >
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-home</v-icon>
            </v-list-item-icon>
            <v-list-item-title>
              <NuxtLink to="/">
                Home
              </NuxtLink>
            </v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-book</v-icon>
            </v-list-item-icon>
            <v-list-item-title>
              <NuxtLink to="/comparetool">
                Compare Tool
              </NuxtLink>
            </v-list-item-title>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>
  <v-app dark>
    <Nuxt />
  </v-app>
  </div>
</template>

<style scoped>

</style>

<script>
export default {
  data: () => ({
    drawer: false,
    group: null,
  }),
}
</script>
