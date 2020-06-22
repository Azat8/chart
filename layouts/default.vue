<template>
  <v-app dark>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
    >
      <v-toolbar-title v-text="title" />
      <v-spacer />
      

      <nuxt-link
        v-if="!this.$auth.user"
        icon
        to="/login"
      >
        <v-btn class="ma-2" outlined color="indigo"><v-icon>mdi-account</v-icon></v-btn>
      </nuxt-link>

      <v-btn 
        v-if="this.$auth.user"
        class="ma-2" 
        outlined 
        color="indigo" 
        @click="logout">
        Logout
      </v-btn>
      <nuxt-link
        v-if="this.$auth.user"
        icon
        to="/chart"
      >
        Chart
      </nuxt-link>

    </v-app-bar>
    <v-main>
      <nuxt />
    </v-main>
  
    <v-footer
      :absolute="!fixed"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>

    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js'
    }
  },
  methods: {
    async logout() {
      await this.$auth.logout()
    }
  }
}
</script>
