<template>
  <Qalendar :events="events" @event-was-clicked="handleEventClick" @edit-event="editEvent" @day-was-clicked="showEventForm" :key="calendarKey" @delete-event="deleteEvent"/>
  <EventForm v-if="showForm" @add-event="addEvent" @close="close"></EventForm>
</template>

<script>
import { Qalendar } from "qalendar";
import 'qalendar/dist/style.css';
import EventForm from '@/components/EventForm.vue';

export default {
  name: 'HomeView',
  components: {
    Qalendar,
    EventForm
  },
  data() {
    return {
      events: [
        {
          title: "Meeting",
          time: { start: "2023-03-26 10:00", end: "2023-03-26 11:00" },
          color: "green",
          id: "1",
          isEditable: true,
        },
        {
          title: "Lunch",
          time: { start: "2023-03-26 12:00", end: "2023-03-26 13:00" },
          color: "red",
          id: "2",
          isEditable: true,
        }
      ],
      showForm: '',
      eventDate: '',
      calendarKey: new Date().getTime(),
      title: '',
      time: '',
      color: '',
      id: '',
      isEditable: true
    }
  },
  methods: {
    handleEventClick(event) {
      console.log(event);
      console.log(event.clickedEvent.title); // выводим в консоль название события
      this.title = event.clickedEvent.title;
      this.time = event.clickedEvent.time;
      this.color = event.clickedEvent.color;
      //console.log(`title ${this.title} time ${this.time.start} color ${this.color}`)
    },
    editEvent(event) {

      // this.events.forEach(el => {
      //   if(el.id == event) {
      //     el.title = 'qwerty'
      //     console.log("Title " + el.title)
      //   }
      // })
      
      this.showForm = true;
    },
    showEventForm(date) {
      this.showForm = true;
      this.eventDate = date;
      console.log(date);
      // this.events.push({
      //   title: 'Test',
      //   time: { start: "2023-03-26 10:00", end: "2023-03-26 11:00" },
      //   color: 'green',
      // });
      // this.calendarKey = new Date().getTime();
      // console.log(this.events)

    },
    addEvent(event) {
      console.log(event);
      const title = event.title;
      const dateStart = event.dateStart;
      const dateEnd = event.dateEnd;
      const timeStart = event.timeStart;
      const timeEnd = event.timeEnd;
      console.log(title, dateStart, dateEnd, timeStart, timeEnd);
      this.events.push({
        title: title,
        time: { start: `${dateStart} ${timeStart}`, end: `${dateEnd} ${timeEnd}`},
        color: 'green',
        id: 3,
        isEditable: true
      });
      this.calendarKey = new Date().getTime();
      console.log(this.events)
      this.showForm = false;
      
    },
    deleteEvent(event) {
      this.events = this.events.filter(el => el.id !== event);
      console.log(this.events);
    },
    close() {
      this.showForm = false;
    }
  }
}
</script>

<style>
</style>
