<template>
<v-app>
    <v-toolbar color="primary" dark fixed app>
        <v-toolbar-title>International Rock Masters</v-toolbar-title>
      </v-toolbar>
 <v-navigation-drawer permanent>
        <v-list>
          <v-list-item class="px-2">
            <v-list-item-avatar size="72">
              <v-img src="https://scontent.fprg1-1.fna.fbcdn.net/v/t39.30808-1/216991861_4284580534941682_5002758828814982599_n.png?stp=dst-png_s200x200&_nc_cat=106&ccb=1-7&_nc_sid=2d3e12&_nc_ohc=4FsoX2jJ4O0Q7kNvgHZpapj&_nc_zt=24&_nc_ht=scontent.fprg1-1.fna&_nc_gid=AA6KjTPaQUjRfMsosw4Ft7k&oh=00_AYDgHiFjFOOGitdYYGOwwUL7b4HIThGaPzyho55lcg2QFw&oe=6771CF32"></v-img>
            </v-list-item-avatar>
          </v-list-item>

          <v-list-item link>
            <v-list-item-content>
              <v-list-item-title class="text-h6">
                {{username || 'Username'}}
              </v-list-item-title>
              <v-list-item-subtitle v-on:click="logout">log out</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-list>

      <v-divider></v-divider>

      <v-list
        dense
        nav
      >
        <v-list-item
          v-for="item in items"
          :key="item.title"
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
</v-app>
</template>

<script>
  export default {
    data () {
      return {
        items: [
          { title: 'Dashboard', icon: 'mdi-view-dashboard' },
          { title: 'Photos', icon: 'mdi-image' },
          { title: 'About', icon: 'mdi-help-box' },
        ],
        username:this.$route.params.username
      }
    },
    methods: {
      logout() {
        this.$router.replace({name:'login'})
      }
    }
  }
</script>