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
      newTask : {
        title: 'кккккккккккк',
        dateStart: '',
        dateEnd: '',
        timeStart: '',
        timeEnd: '',
      }
    }
  },
  methods: {
    handleEventClick(event) {
      console.log(event);
      console.log(event.clickedEvent.title); // выводим в консоль название события
      this.newTask.title = event.clickedEvent.title;
      const time = event.clickedEvent.time;
      //console.log(time);
      console.log(time.start);
      console.log(time.end);
      
      const dateStart = time.start;
      const dateEnd = time.end;
      const dateTimeStart = new Date(dateStart)
      const dateTimeEnd = new Date(dateEnd);
      //console.log(dateTimeStart);
      const yearStart = dateTimeStart.getFullYear();
      const yearEnd = dateTimeEnd.getFullYear();
      //console.log(`year ${yearStart}`);
      const monthStart = dateTimeStart.getMonth() + 1;
      const monthEnd = dateTimeEnd.getMonth() + 1;
      //console.log(`month ${monthStart}`);
      const dayStart = dateTimeStart.getDate();
      const dayEnd = dateTimeEnd.getDate();
     // console.log(`day ${dayStart} ${typeof(dayStart)}`)
      const dateStartOne = `${yearStart}-${monthStart < 10 ? '0' + monthStart : monthStart}-${dayStart < 10 ? '0' + dayStart : dayStart}`;
      const dateEndOne = `${yearEnd}-${monthEnd < 10 ? '0' + monthEnd : monthEnd}-${dayEnd < 10 ? '0' + dayEnd : dayEnd}`;
      // console.log(`итог ${dateStartOne}`);
      // console.log(`итог 2 ${dateEndOne}`)
      const hoursStart = dateTimeStart.getHours();
      const hoursEnd = dateTimeEnd.getHours();
      const minutesStart = dateTimeStart.getMinutes();
      const minutesEnd = dateTimeEnd.getMinutes();
      const dateStartTwo = `${hoursStart < 10 ? '0' + hoursStart : hoursStart}:${minutesStart < 10 ? '0' + minutesStart : minutesStart}`
      const dateEndTwo = `${hoursEnd < 10 ? '0' + hoursEnd : hoursEnd}:${minutesEnd < 10 ? '0' + minutesEnd : minutesEnd}`;
      const str = dateStartOne + ' ' + dateStartTwo; 
      const str2 = dateEndOne + ' ' + dateEndTwo;
      //this.newTask.color = event.clickedEvent.color;
      this.newTask.dateStart = dateStartOne;
      this.newTask.dateEnd = dateEndOne;
      this.newTask.timeStart = dateStartTwo;
      this.newTask.timeEnd = dateEndTwo;
      console.log(this.newTask);
      //console.log(`title ${this.newTask.title} timeStart ${this.dateStart} ${this.timeStart} timeEnd ${this.dateEnd} ${this.timeEnd}`);
     
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
        id: new Date(),
        isEditable: true
      });
      this.calendarKey = new Date().getTime();
      console.log(this.events)
      this.showForm = false;
      
    },
    deleteEvent(event) {
      this.events = this.events.filter(el => el.id !== event);
      //console.log(this.events);
    },
    close() {
      this.showForm = false;
    },
    
  },
  
}
</script>

<style>
</style>
