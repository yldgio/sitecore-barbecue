/* eslint-disable vue/valid-v-on */ /* eslint-disable vue/no-v-html */ /*
eslint-disable vue/no-v-html */
<template>
  <v-col sm="10" md="9" lg="11">
    <v-card>
      <v-parallax dark height="300" src="/bbq-bg2.jpg">
        <v-row align="center" justify="center">
          <v-col class="text-center text-shadow" cols="12">
            <h1 class="headline">
              Sitecore Barbecue ...the Communiters SPA
            </h1>
            <h4 class="subheading">
              Join us for a free drink... we will provide the meat!
            </h4>
          </v-col>
        </v-row></v-parallax
      >
        <v-alert
          outlined
          type="warning"
          prominent
          border="left"
          close-text="Chiudi" 
          dismissible>
          Gentili Communiters, a causa dell'epidemia di coronavirus (COVID-19) non saremo in grado di garantire carne per tutti
        </v-alert>
      <nuxt-child />
    </v-card>
  </v-col>
</template>

<script>
import axios from "axios";
// import Logo from "~/components/Logo.vue";
// import SitecoreLogo from "~/components/SitecoreLogo.vue";
process.env.NODE_TLS_REJECT_UNAUTHORIZED = "0";

export default {
  components: {
    // Logo,
    // SitecoreLogo
  },
  asyncData({ params }) {
    return axios
      .get(
        "https://communiters-dev.westeurope.cloudapp.azure.com/_api/speakers?sc_device=json"
      )
      .then(res => {
        return { people: res.data.data };
      });
  }
};
</script>
<style scoped>
.people li a {
  display: block;
  border: 1px #ddd solid;
  padding: 10px;
  text-align: left;
  color: #222;
  text-decoration: none;
}
.people li a:hover {
  color: orange;
}
</style>
