<template>
  <div>
     <v-row class="fill-height">
    <v-col>

      <v-sheet height="64">
        <v-toolbar flat>
          <v-btn outlined class="mr-4" color="grey darken-2" @click="setToday">Today</v-btn>
          <v-btn fab text small color="grey darken-2" @click="prev">
            <v-icon small> mdi-chevron-left </v-icon>
          </v-btn>
          <v-btn fab text small color="grey darken-2" @click="next">
            <v-icon small>mdi-chevron-right</v-icon>
          </v-btn>
          <v-toolbar-title v-if="$refs.calendar"> {{ $refs.calendar.title }} </v-toolbar-title>
          <v-spacer></v-spacer>
          <v-menu bottom right>
            <template v-slot:activator="{ on, attrs }">
              <v-btn outlined color="grey darken-2" v-bind="attrs" v-on="on">
                <span>{{ typeToLabel[type] }}</span>
                <v-icon right> mdi-menu-down </v-icon>
              </v-btn>
            </template>
            <v-list>
              <v-list-item @click="type = 'category'"><v-list-item-title>Staff</v-list-item-title></v-list-item>
              <v-list-item @click="type = 'month'"><v-list-item-title>Month</v-list-item-title></v-list-item>
              <v-list-item @click="type = 'week'"><v-list-item-title>Week</v-list-item-title></v-list-item>
              <v-list-item @click="type = '4day'"><v-list-item-title>4 days</v-list-item-title></v-list-item>
              <v-list-item @click="type = 'day'"><v-list-item-title>Day</v-list-item-title></v-list-item>
            </v-list>
          </v-menu>
        </v-toolbar>
      </v-sheet>

      <v-sheet height="600">
        <v-calendar ref="calendar" v-model="focus" color="red" :type="type" category-show-all 
        :categories="categories" :events="events" :event-color="getEventColor">
        <template v-slot:event="{ eventSummary }">
            <div class="v-event-draggable" v-html="eventSummary()"></div>
          </template>
        </v-calendar>
      </v-sheet>

    </v-col>
  </v-row>
  </div>
</template>

<script>
  export default {
    name: 'HelloWorld',

    data: () => ({
      focus: '',
      type: 'category',
      typeToLabel: { month: 'Month', week: 'Week', day: 'Day', '4day': '4 Days', category: "category"},
      events: [],
      fromDataBase: [
        {id:1, title: "Hair Cut", start: "2020-11-18 08:00", end: "2020-11-18 12:30", allDay: false, backgroundColor:"red", category:'John Smith' },
        {id:2, title: "Shave", start: "2020-11-18 16:30", end: "2020-11-18 21:00", allDay: false, backgroundColor:"indigo", category:'Goku'},
        {id:3, title: "Hair Color", start: "2020-11-18 16:30", end: "2020-11-18 21:00", allDay: false, backgroundColor:"green", category:'Goku'},
        {id:4, title: "Full course", start: "2020-11-18 16:30", end: "2020-11-18 21:00", allDay: false, backgroundColor:"indigo", category:'Tori Walker'},
        {id:5, title: "Full course", start: "2020-11-18 16:30", end: "2020-11-18 21:00", allDay: false, backgroundColor:"pink", category:'Tori Walker'},
      ],
      colors: ['blue', 'indigo', 'deep-purple'],
      names: ['Meeting', 'Holiday', 'PTO', 'Travel', 'Event', 'Birthday', 'Conference', 'Party'],
      categories: ['John Smith', 'Tori Walker', 'Goku'],
    }),
    mounted () {
      this.fetchEvents();
    },
    methods: {
      getEventColor (event) {
        return event.color
      },
      setToday () {
        this.focus = ''
      },
      prev () {
        this.$refs.calendar.prev()
      },
      next () {
        this.$refs.calendar.next()
      },
      fetchEvents () { 
        for (let i = 0; i < this.fromDataBase.length; i++) {
          this.events.push({
            name: `${this.fromDataBase[i].title} by ${this.fromDataBase[i].category}` ,
            start: this.fromDataBase[i].start,
            end: this.fromDataBase[i].end,
            color: this.fromDataBase[i].backgroundColor,
            allDay: this.fromDataBase[i].allDay,
            category: this.fromDataBase[i].category,
          })
        }
        //this.events = events
      },
      rnd (a, b) {
        return Math.floor((b - a + 1) * Math.random()) + a
      },
    },
  }
</script>

<style scoped lang="scss">
.v-event-draggable {
  text-align: center;
  font-family: 'Courier New', Courier, monospace;
}

</style>