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
      md6
    >
      <div class="text-center">
        <logo />
        <sitecore-logo />
      </div>
      <v-card>
        <v-card-title class="headline">
          Communiters SPA ...Single Page Application!
        </v-card-title>
        <v-list three-line>
          <template v-for="item in people">
            <v-list-item
              :key="item.id"
            >
              <v-list-item-avatar>
                <v-img :src="'http://ibl-dev-02.westeurope.cloudapp.azure.com/' + item.profile_image" />
              </v-list-item-avatar>

              <v-list-item-content>
                <v-list-item-title v-text="item.full_name" />
                <v-list-item-subtitle v-text="item.role" />
                <v-list-item-content>
                  <p>{{ item.email }}</p>
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
            to="/inspire"
          >
            Continue
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
export default {
  components: {
    Logo,
    SitecoreLogo
  },
  asyncData ({ params }) {
    return axios.get('http://ibl-dev-02.westeurope.cloudapp.azure.com/api/people?sc_device=json')
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
