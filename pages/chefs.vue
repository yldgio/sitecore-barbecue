<template>
  <v-layout>
    <v-flex class="text-center">
      <img
        src="/v.png"
        alt="Vuetify.js"
        class="mb-5"
      >
      <v-card>
        <v-card-title class="headline">
          Gli Chef
        </v-card-title>
        <v-list three-line>
          <template v-for="item in chefs">
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
      </v-card>
    </v-flex>
  </v-layout>
</template>
<script>
import axios from 'axios'
process.env.NODE_TLS_REJECT_UNAUTHORIZED = '0'
export default {
  asyncData ({ params }) {
    return axios.get('https://communiters-dev.westeurope.cloudapp.azure.com/_api/speakers?sc_device=json')
      .then((res) => {
        return { chefs: res.data.data }
      })
  }
}
</script>
