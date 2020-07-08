<template>
  <v-container class="fill-height" fluid style="min-height: 434px">
    <v-fade-transition mode="out-in">
      <v-row v-if="show" key="0">
        <v-col cols="12">
          <v-card>
            <v-img
              src="/bbq-bg.jpg"
              height="425"
              contain
              class="grey darken-4"
            />
            <v-card-title class="title">
              Sitecore Barbecue ...the Communiters SPA
            </v-card-title>
          </v-card>
        </v-col>
      </v-row>
    </v-fade-transition>
  </v-container>
</template>
<script>
export default {
  data: () => ({
    show: true
  })
};
</script>
