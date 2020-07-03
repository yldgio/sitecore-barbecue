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
          Le ricette
        </v-card-title>
        <v-list three-line>
          <template v-for="item in recipes">
            <v-list-item
              :key="item.id"
            >
              <v-list-item-content>
                <v-list-item-title v-text="item.title" />
                <v-list-item-subtitle v-text="item.short_description" />
                <v-list-item-content>
                  <p>{{ item.long_description }}</p>
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
export default {
  asyncData ({ params }) {
    return axios.get('http://communiters-dev.westeurope.cloudapp.azure.com/_api/speeches?sc_device=json')
      .then((res) => {
        return { recipes: res.data.data }
      })
  }
}
</script>
