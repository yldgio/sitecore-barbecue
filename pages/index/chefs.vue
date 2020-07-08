<template>
  <v-flex>
    <v-card-subtitle class="headline d-flex justify-center align-baseline">
      <v-icon v-text="'mdi-chef-hat pr-2'" /> Gli Chef
    </v-card-subtitle>
    <v-container fluid>
      <v-row>
        <v-col v-for="item in chefs" :key="item.id" :cols="6">
          <v-card>
            <div class="relative">
              <v-img
                :src="
                  'http://communiters-dev.westeurope.cloudapp.azure.com' +
                    item.picture
                "
                class="white--text align-end"
                gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                height="200px"
              >
                <v-card-title v-text="item.fullname"></v-card-title>
              </v-img>
              <v-dialog v-model="dialog" width="500">
                <template v-slot:activator="{ on, attrs }">
                  <v-btn
                    fab
                    dark
                    small
                    color="red accent-4"
                    absolute
                    right
                    bottom
                    v-bind="attrs"
                    v-on="on"
                  >
                    <v-icon>mdi-book-information-variant</v-icon>
                  </v-btn>
                </template>

                <v-card>
                  <v-list-item>
                    <v-list-item-avatar>
                      <img
                        :src="
                          'http://communiters-dev.westeurope.cloudapp.azure.com' +
                            item.thumbnail
                        "
                      />
                    </v-list-item-avatar>
                    <v-list-item-content>
                      <v-list-item-title
                        class="headline"
                        v-text="item.fullname"
                      />
                      <v-list-item-subtitle v-text="item.title" />
                    </v-list-item-content>
                  </v-list-item>
                  <v-card-text v-text="item.bio" />
                </v-card>
              </v-dialog>
            </div>
            <v-card-subtitle v-text="item.title" />
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-flex>
</template>
<script>
import axios from "axios";
process.env.NODE_TLS_REJECT_UNAUTHORIZED = "0";
export default {
  asyncData({ params }) {
    return axios
      .get(
        "https://communiters-dev.westeurope.cloudapp.azure.com/_api/speakers?sc_device=json"
      )
      .then(res => {
        return { chefs: res.data.data };
      });
  }
};
</script>
<style scoped>
.relative {
  position: relative;
}
</style>
