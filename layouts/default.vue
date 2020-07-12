<template>
  <v-app>
    <v-navigation-drawer v-model="drawer" clipped fixed app expand-on-hover>
      <v-list :mini-variant="miniVariant" @hover="true">
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title v-text="title" />
      <v-spacer />
      
    </v-app-bar>
    <v-content>
      <v-container>
        <v-row column justify="center" align-content="center">
          <nuxt />
        </v-row>
      </v-container>
    </v-content>
    <v-footer :absolute="!fixed" app>
      <span>Communiters &copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: true,
      fixed: true,
      drawer: false,
      items: [
        {
          icon: "mdi-food-steak",
          title: "Benvenuti",
          to: "/"
        },
        {
          icon: "mdi-chef-hat",
          title: "Gli Chef",
          to: "/chefs"
        },
        {
          icon: "mdi-order-bool-descending-variant",
          title: "Le ricette",
          to: "/recipes"
        },
        {
          icon: "mdi-calendar-clock",
          title: "Gli appuntamenti",
          to: "/calendar"
        }
      ],
      miniVariant: true,
      title: "Sitecore Barbecue - Communiters on SPA"
    };
  }
};
</script>
