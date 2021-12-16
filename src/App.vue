<template>
  <v-app>
    <v-navigation-drawer v-model="drawer" app>
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="text-h6">Vuetify Todo</v-list-item-title>
          <v-list-item-subtitle>Best Todo Ever!</v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" link :to="item.to">
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app dark color="primary" src="snowflakes.jpg" shrink-on-scroll>
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,0.3), rgba(128,208,199,0.5)"
        ></v-img>
      </template>

      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>Vuetify Todo</v-toolbar-title>
      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-heart</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <v-container fluid class="pa-0">
        <router-view></router-view>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      drawer: null,
      items: [
        {
          title: "Todo",
          icon: "mdi-format-list-checks",
          to: "/",
        },
        {
          title: "About",
          icon: "mdi-help-box",
          to: "/about",
        },
      ],
    };
  },
};
</script>
