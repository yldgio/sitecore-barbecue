<template>
  <v-flex>
    <v-card-subtitle class="headline d-flex justify-center align-baseline">
      <v-icon v-text="'mdi-food-steak pr-2'" />Benvenuti barbecuers Communiters
    </v-card-subtitle>
    <v-container fluid>
      <v-row>
        <v-col cols="12">
          <h3>Sitecore Communiters (on barbecue)</h3>
          <p>la comunità italiana di Sitecore dedicata a Clienti e Partners.</p>
          <p>
            L’iniziativa vuole promuovere, nel contesto italiano, dei momenti di discussione e condivisione intorno a Sitecore con una modalità informale ed incisiva:
            quattro storie concrete da raccontare e al termine un aperitivo dove far circolare idee e conoscersi di più.
          </p>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="6">
          <v-carousel cycle>
            <v-carousel-item
              v-for="(item,i) in items"
              :key="i"
              :src="item.src"
              reverse-transition="fade-transition"
              transition="fade-transition"
            ></v-carousel-item>
          </v-carousel>
        </v-col>
        <v-col cols="6">
          <p>Alla luce dei fatti di queste settimane, il primo evento non potrà chiaramente realizzarsi come l’avevamo pensato, ma in questo periodo abbiamo continuato a lavorare sull’iniziativa in funzione di come il contesto intorno a noi, professionale e personale, stava cambiando. Valutando il percorso migliore per reagire e non restare a guardare.</p>
          <p>Da tutto questo è nata l’idea di ‘Open Mic’: un punto di contatto per esser più vicini a clienti e a partner di Sitecore per metter a fattor comune esperienze di questi giorni, per dargli voce e supporto.</p>
          <p>Potrai decidere se contattarci per raccontarci come stai affrontando questo periodo e magari esser disposto a condividere la tua esperienza anche con altri clienti come te, in un prossimo evento virtuale e interattivo.</p>
          <p>Oppure potrai suggerirci qual è il tema strategico, di business o tecnico intorno a Sitecore che ti sta più a cuore e che ti piacerebbe vedere approfondito dagli esperti della comunità in un prossimo evento per i Communiters.</p>
          <p>Facci sapere, il microfono è acceso.
            <v-btn class="mx-2" fab dark small color="red" href="https://calendly.com/sitecore-italia/open-mic">
              <v-icon dark>mdi-calendar-clock</v-icon>            
            </v-btn>
          </p>          
          <p>
            Dario, Federico, Giovanni, Marcello
            (ovvero il consiglio dei Communiters)
          </p>        
        </v-col>
      </v-row>
    </v-container>
  </v-flex>
</template>
<script>
export default {
  data() {
    return {
      items: [
        {
          src: "/barbecue-1.jpeg"
        },
        {
          src: "/barbecue-2.jpeg"
        },
        {
          src: "/barbecue-3.jpeg"
        },
        {
          src: "/barbecue-4.jpeg"
        },
        {
          src: "/barbecue-5.jpeg"
        }
      ]
    };
  }
};
</script>
