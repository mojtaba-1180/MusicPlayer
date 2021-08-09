<template>
  <v-app>
    <v-system-bar window dark></v-system-bar>
    <v-app-bar
      fixed
      flat
      style="border-bottom:1px solid #aaa !importnat"
    >
      <div class="d-flex align-center">
              <v-app-bar-nav-icon @click=" /*miniVariant = !miniVariant; */drawer = !drawer; " ></v-app-bar-nav-icon>
      </div>
      <v-spacer></v-spacer>
      <v-switch
        v-model="$vuetify.theme.dark"
        inset
      ></v-switch>
     <div class="d-flex justify-center my-5">
        <v-avatar color="primary" >
          <span class="white--text text-h5">MY</span>
        </v-avatar>
        </div>
    </v-app-bar>
    <v-navigation-drawer
      style="z-index:1;"
      v-model="drawer"
      class="pt-15"
      color="gray lighten-5"
      :mini-variant="miniVariant"
      app
    >
    <v-text-field
    class="mx-2 my-4"
    outlined
    label="Search..."
    append-icon="mdi-magnify"
    flat>
    </v-text-field>
      <v-list-item-group>
        <v-list-item
          color="primary"
          class="mx-3 py-0 rounded-lg my-2"
          v-for="item in items"
          :key="item.title"
          :to="item.link"
        >
          <v-list-item-content>
            <v-list-item-title >{{item.title}}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list-item-group>

      <template v-slot:append>
        <div class="pa-2">
          <v-btn block>
            <v-icon left>mdi-export</v-icon>
            Logout
          </v-btn>
        </div>
      </template>
    </v-navigation-drawer>
    <v-main class="mt-15" >
       <transition name="slide-fade">
      <router-view> </router-view>
       </transition>
    </v-main>
  </v-app>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      drawer: true,
      miniVariant: false,
      items: [
        { title: 'Dashboard', icon: 'mdi-view-dashboard', link: '/' },
        { title: 'About', icon: 'mdi-account-box', link: '/about' },
        { title: 'Admin', icon: 'mdi-gavel' }
      ]
    }
  },
  methods: {
    getData () {
      const config = {
        method: 'get',
        url: 'https://bazigift.com/wp-json/wc/v3/products',
        headers: { 
          'Authorization': 'Basic Y2tfN2IwZWU1NWJiMmNlY2ZjNGJkYzZlZWRiZjU1YzA2MTllNGMxYzhhNzpjc18yYmJlNjI3MzBkYjJmYWU4ZDUxNzk1YTIxNDdlZTY5ZDI2NDAyYmJi', 
          'Cookie': 'PHPSESSID=d9f9bb3d392c91c3f5567577d9869f94'
        }
      };
      axios(config)
      .then((response) => {
        console.log(JSON.stringify(response.data));
      })
      .catch((error) => {
        console.log(error);
      });

    }
  },
  mounted () {
    this.getData()
  }
}
</script>
<style>
  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s;
  }
  .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
    opacity: 0;
  }
  .slide-fade-enter-active {
    transition: all .3s ease .3s;
  }
  .slide-fade-leave-active {
    transition: all .2s cubic-bezier(1.0, 0.5, 0.8, 1.0);
  }
  .slide-fade-enter, .slide-fade-leave-to
  /* .slide-fade-leave-active below version 2.1.8 */ {
    transform: translateX(10px);
    opacity: 0;
  }
</style>
