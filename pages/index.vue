/* eslint-disable vue/valid-v-on */
/* eslint-disable vue/no-v-html */
/* eslint-disable vue/no-v-html */
<template>
  <v-layout
    column
    justify-center
    align-center
  >
    <v-flex
      xs12
      sm8
      md8
    >
      <div class="text-center">
        <logo />
        <sitecore-logo />
      </div>
      <v-card>
        <v-card-title class="headline">
          Sitecore Barbecue ...the Commuiters SPA
        </v-card-title>
        <v-list three-line>
          <template v-for="item in people">
            <v-list-item
              :key="item.id"
            >
              <v-list-item-avatar>
                <v-img :src="'http://communiters-dev.westeurope.cloudapp.azure.com' + item.thumbnail" />
              </v-list-item-avatar>
              <v-list-item-content>
                <v-list-item-title v-text="item.fullname" />
                <v-list-item-subtitle v-text="item.title" />
                <v-list-item-content>
                  <p>{{ item.bio }}</p>
                </v-list-item-content>
              </v-list-item-content>
            </v-list-item>
          </template>
        </v-list>
        <v-card-actions>
          <v-spacer />
          <v-btn
            color="primary"
            nuxt
            to="/Events"
          >
            Events
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import axios from 'axios'
import Logo from '~/components/Logo.vue'
import SitecoreLogo from '~/components/SitecoreLogo.vue'
process.env.NODE_TLS_REJECT_UNAUTHORIZED = '0'

export default {
  components: {
    Logo,
    SitecoreLogo
  },
  asyncData ({ params }) {
    return axios.get('https://communiters-dev.westeurope.cloudapp.azure.com/_api/speakers?sc_device=json')
      .then((res) => {
        return { people: res.data.data }
      })
  }
}
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
