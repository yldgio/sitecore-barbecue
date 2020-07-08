<template>
  <v-flex>
    <v-col>
      <v-card-subtitle class="headline d-flex justify-center align-baseline">
        <v-icon v-text="'mdi-calendar-clock pr-2'" />Gli appuntamenti
      </v-card-subtitle>

      <v-toolbar flat color="white">
        <v-btn outlined class="mr-4" color="grey darken-2" @click="setToday">
          Today
        </v-btn>
        <v-btn fab text small color="grey darken-2" @click="prev">
          <v-icon small>
            mdi-chevron-left
          </v-icon>
        </v-btn>
        <v-btn fab text small color="grey darken-2" @click="next">
          <v-icon small>
            mdi-chevron-right
          </v-icon>
        </v-btn>
        <v-toolbar-title v-if="$refs.calendar">
          {{ $refs.calendar.title }}
        </v-toolbar-title>
        <v-spacer />
        <v-menu bottom right>
          <template v-slot:activator="{ on, attrs }">
            <v-btn outlined color="grey darken-2" v-bind="attrs" v-on="on">
              <span>{{ typeToLabel[type] }}</span>
              <v-icon right>
                mdi-menu-down
              </v-icon>
            </v-btn>
          </template>
          <v-list>
            <v-list-item @click="type = 'day'">
              <v-list-item-title>Day</v-list-item-title>
            </v-list-item>
            <v-list-item @click="type = 'week'">
              <v-list-item-title>Week</v-list-item-title>
            </v-list-item>
            <v-list-item @click="type = 'month'">
              <v-list-item-title>Month</v-list-item-title>
            </v-list-item>
            <v-list-item @click="type = '4day'">
              <v-list-item-title>4 days</v-list-item-title>
            </v-list-item>
          </v-list>
        </v-menu>
      </v-toolbar>
      <v-calendar
        ref="calendar"
        v-model="focus"
        color="primary"
        :events="events"
        :event-color="getEventColor"
        :type="type"
        @click:event="showEvent"
        @click:more="viewDay"
        @click:date="viewDay"
        @change="updateRange"
      />
      <v-dialog v-model="selectedOpen" width="900" scrollable>
        <v-card>
          <v-toolbar :color="selectedEvent.color" dark>
            <v-btn icon>
              <v-icon>mdi-microphone-variant</v-icon>
            </v-btn>
            <v-toolbar-title v-text="selectedEvent.name" />
            <v-spacer />
            <v-btn icon>
              <v-icon>mdi-heart</v-icon>
            </v-btn>
            <v-btn icon>
              <v-icon>mdi-dots-vertical</v-icon>
            </v-btn>
          </v-toolbar>
          <v-list three-line>
            <template v-for="item in selectedEvent.speeches">
              <v-list-item :key="item.name">
                <v-list-item-avatar>
                  <img
                    :src="
                      'http://communiters-dev.westeurope.cloudapp.azure.com' +
                        item.speaker.thumbnail
                    "
                  />
                </v-list-item-avatar>
                <v-list-item-content>
                  <v-list-item-title class="headline" v-text="item.title" />
                  <v-list-item-subtitle v-text="item.short_description" />
                </v-list-item-content>
              </v-list-item>
              <v-divider :key="`divider-${item.title}`" />
            </template>
          </v-list>
          <v-card-text v-html="selectedEvent.description" />
        </v-card>
      </v-dialog>
    </v-col>
  </v-flex>
</template>
<script>
import axios from "axios";
process.env.NODE_TLS_REJECT_UNAUTHORIZED = "0";
export default {
  asyncData({ params }) {
    return axios
      .get(
        "https://communiters-dev.westeurope.cloudapp.azure.com/_api/events?sc_device=json"
      )
      .then(res => {
        const evts = res.data.data.map(itm => {
          const dt = new Date(`${itm.date}T${itm.time}`);
          const endt = new Date(dt.getTime() + 60 * 60 * 1000);
          return {
            name: itm.title,
            start: dt,
            end: endt,
            color: "blue",
            timed: true,
            speeches: itm.speeches,
            description: itm.description.replace(/(\\r)*\\n/g, "<br>")
          };
        });
        return { events: evts };
      });
  },
  data: () => ({
    focus: "",
    type: "month",
    typeToLabel: {
      month: "Month",
      week: "Week",
      day: "Day",
      "4day": "4 Days"
    },
    selectedEvent: {},
    selectedElement: null,
    selectedOpen: false,
    // events: [],
    colors: [
      "blue",
      "indigo",
      "deep-purple",
      "cyan",
      "green",
      "orange",
      "grey darken-1"
    ],
    names: [
      "Meeting",
      "Holiday",
      "PTO",
      "Travel",
      "Event",
      "Birthday",
      "Conference",
      "Party"
    ]
  }),
  mounted() {
    this.$refs.calendar.checkChange();
  },
  methods: {
    viewDay({ date }) {
      this.focus = date;
      this.type = "day";
    },
    getEventColor(event) {
      return "green";
      // event.color
    },
    setToday() {
      this.focus = "";
    },
    prev() {
      this.$refs.calendar.prev();
    },
    next() {
      this.$refs.calendar.next();
    },
    showEvent({ nativeEvent, event }) {
      const open = () => {
        this.selectedEvent = event;
        this.selectedElement = nativeEvent.target;
        setTimeout(() => {
          this.selectedOpen = true;
        }, 10);
      };

      if (this.selectedOpen) {
        this.selectedOpen = false;
        setTimeout(open, 10);
      } else {
        open();
      }

      nativeEvent.stopPropagation();
    },
    updateRange({ start, end }) {
      /* const events = []

      const min = new Date(`${start.date}T00:00:00`)
      const max = new Date(`${end.date}T23:59:59`)
      const days = (max.getTime() - min.getTime()) / 86400000
      const eventCount = this.rnd(days, days + 20)

      for (let i = 0; i < eventCount; i++) {
        const allDay = this.rnd(0, 3) === 0
        const firstTimestamp = this.rnd(min.getTime(), max.getTime())
        const first = new Date(firstTimestamp - (firstTimestamp % 900000))
        const secondTimestamp = this.rnd(2, allDay ? 288 : 8) * 900000
        const second = new Date(first.getTime() + secondTimestamp)

        events.push({
          name: this.names[this.rnd(0, this.names.length - 1)],
          start: first,
          end: second,
          color: this.colors[this.rnd(0, this.colors.length - 1)],
          timed: !allDay
        })
      }

      this.events = events */
    },
    rnd(a, b) {
      return Math.floor((b - a + 1) * Math.random()) + a;
    }
  }
};
</script>
