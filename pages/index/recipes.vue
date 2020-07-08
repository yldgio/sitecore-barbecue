<template>
  <v-flex>
    <v-card-subtitle class="headline d-flex justify-center align-baseline">
      <v-icon v-text="'mdi-order-bool-descending-variant pr-2'" /> Le ricette
    </v-card-subtitle>
    <v-list three-line>
      <template v-for="item in recipes">
        <v-list-item :key="item.id">
          <v-list-item-avatar>
            <v-img
              :src="
                '//communiters-dev.westeurope.cloudapp.azure.com' +
                  item.speaker.picture
              "
            />
          </v-list-item-avatar>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
            <v-list-item-subtitle v-text="item.short_description" />
            <v-list-item-content>
              <p>{{ item.long_description }}</p>
            </v-list-item-content>
          </v-list-item-content>
        </v-list-item>
        <v-divider :key="`divider-${item.id}`" />
      </template>
    </v-list>
  </v-flex>
</template>
<script>
import axios from "axios";
process.env.NODE_TLS_REJECT_UNAUTHORIZED = "0";
export default {
  asyncData({ params }) {
    return axios
      .get(
        "https://communiters-dev.westeurope.cloudapp.azure.com/_api/speeches?sc_device=json"
      )
      .then(res => {
        return { recipes: res.data.data };
      });
  }
};
</script>
