<template>
  <div class="calendar">
    <FullCalendar :options="calendarOptions"/>
  </div>
</template>

<script>
require('@fullcalendar/daygrid/main.min.css')
require('@fullcalendar/timegrid/main.min.css')

import FullCalendar from "@fullcalendar/vue";
import DayGrid from "@fullcalendar/daygrid";
import TimeGrid from "@fullcalendar/timegrid";
import Interaction from "@fullcalendar/interaction";
//import { createEventId } from "./event-utils";


export default {
  name: 'Calendar',
  components: { FullCalendar },
  data() {
    return {
      calendarOptions: { 
        plugins: [ TimeGrid, DayGrid, Interaction ],
        initialView: 'timeGridDay' ,
        headerToolbar: { left: "title", center: "dayGridMonth,timeGridWeek,timeGridDay", right: "prev today next",},
        selectable: true,
        events: [
              {id:1, user: 'brian', title: "Something", start: "2020-11-17T08:00:00+06:00", end: "2020-11-17T12:30:00+06:00", allDay: false, backgroundColor:"#bce6eb", textColor: "#30475e" },
              {id:2, user: 'bri', title: "Nothing", start: "2020-11-17T12:30:00+06:00", end: "2020-11-17T13:00:00+06:00", allDay: false, backgroundColor:"black", textColor: "#ddd"},
              {id:3, title: "Nothing", start: "2020-11-17T21:30:00+06:00", end: "2020-11-17T24:00:00+06:00", allDay: false, }
        ], 
        //eventClick: this.handleEventClick,
        //eventsSet: this.handleEvents,
        //select: this.handleSelect,
        },
        // Data: [
        //       {id:1, title: "Something", start: "2020-11-17T08:00:00+06:00", end: "2020-11-17T12:30:00+06:00", allDay: false,},
        //       {id:2, title: "Nothing", start: "2020-11-17T16:30:00+06:00", end: "2020-11-17T21:00:00+06:00", allDay: false,}
        // ],
    }
  },
  methods: {
    // handleSelect(arg){
    //   console.log(JSON.stringify(arg))
    //   let title = prompt('Please enter a new title for your event')
    //   console.log(title)
    //   let calendarApi = arg.view.calendar
    //   calendarApi.unselect() // clear date selection
    //   if (title) {
    //     calendarApi.addEvent({
    //       //id: createEventId(),
    //       title,
    //       start: arg.startStr,
    //       end: arg.endStr,
    //       allDay: arg.allDay
    //     })
    //   }
    // },
    // handleEvents(events) {
    // //this.events = events;
    // //console.log("handleEvents -> events", JSON.stringify(this.events))   
    // //console.log(this.events[0].title)   
    
    // }
  }
}
</script>

<style scoped>

</style>
