<template>
  <v-app id="inspire" >
    <v-navigation-drawer
      v-model="drawer"
      :mobile-breakpoint="768"
      app
      v-if="isAuthenticated"
    >
      <v-img
        class="pa-4 pt-7"
        src="rockMusic.jpg"
        height="170"
        gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
      >
        <v-avatar size="70" class="mb-2">
          <img
            src="https://myhotposters.com/cdn/shop/products/mQ0284_large.jpeg?v=1571444134"
            alt="masterOfRock"
          > 
        </v-avatar>
        <div class="white--text text-subtitle-1 font-weight-bold">
        {{ username }}
        </div>
        <div v-on:click="logout" class="white--text text-subtitle-2" style="cursor: pointer; font-style: italic;">
          logout
        </div>
      </v-img>

  



      <v-list
        dense
        nav
      >
        <v-list-item
          v-for="item in items"
          :key="item.title"
          :to="item.to"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      color="primary"
      dark
      src="rockMusic2.jpg"
      prominent
      :height="$route.path === '/' ? '238' : '170'"
      v-if="isAuthenticated"
    >
      <template v-slot:img="{ props }"
      >
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.9), rgba(148,61,15,.9)"
        ></v-img>
      </template>

      <v-container class="header-container pa-0"
      >
        <v-row>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <search />
        </v-row>
        <v-row>
          <v-toolbar-title class="text-h4 ml-4">
            {{ $store.state.appTitle }}
          </v-toolbar-title>
        </v-row>
        <v-row>
          <live-date-time />
        </v-row>
        <v-row v-if="$route.path === '/'">
          <field-add-task />
        </v-row>
      </v-container>

    </v-app-bar>

    <v-main>
      <router-view></router-view>
      <snackbar />
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ({
      drawer: null,
      items: [
        { title: 'Bucket List', icon: 'mdi-format-list-checks', to: '/' },
        { title: 'About', icon: 'mdi-help-box', to: '/about' },
      ],
    }),
    mounted() {
      this.$store.dispatch('getTasks')
    },
    components: {
      'search': require('@/components/Tools/Search.vue').default,
      'live-date-time': require('@/components/Tools/LiveDateTime.vue').default,
      'field-add-task': require('@/components/BucketList/FieldAddTask.vue').default,
      'snackbar': require('@/components/Shared/Snackbar.vue').default
    },
    methods: {
      logout() {
        this.$router.replace({name:'login'})
      }
    },
    computed: {
    isAuthenticated() {
      // Add your authentication logic here
      return this.$route.name !== 'login'
    },
    username() {
      return this.$route.params.username
    }
    }
  }
</script>

<style lang="sass">
  .header-container
    max-width: none
</style>