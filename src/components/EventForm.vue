<template>
    <div class="event-form-modal">
      <div class="event-form-wrapper">
        <form @submit.prevent="submitEvent" class="event-form">
          <div class="form-group">
            <label for="title">Title:</label>
            <input v-model="event.title" type="text" id="title" required>
          </div>
          <div class="form-group">
            <label for="dateStart">Start date:</label>
            <input v-model="event.dateStart" type="date" id="dateStart" required>
          </div>
          <div class="form-group">
            <label for="dateEnd">End date:</label>
            <input v-model="event.dateEnd" type="date" id="dateEnd" required>
          </div>
          <div class="form-group">
            <label for="timeStart">Start time:</label>
            <input v-model="event.timeStart" type="time" id="timeStart" required>
          </div>
          <div class="form-group">
            <label for="timeEnd">End time:</label>
            <input v-model="event.timeEnd" type="time" id="timeEnd" required>
          </div>
          <div class="form-group">
            <button type="submit">Add Event</button>
          </div>
        </form>
        <button class="close-button" @click="$emit('close')">X</button>
      </div>
    </div>
  </template>
  
<script>
    export default {
    data() {
      return {
        event: {
          title: '',
          dateStart: '',
          dateEnd: '',
          timeStart: '',
          timeEnd: ''
        }
      }
    },
    methods: {
      submitEvent() {
        this.$emit('add-event', this.event);
        this.event.title = '';
        this.event.date = '';
        this.event.time = '';
      },
      
    }
  }
</script>
 
<style>
.event-form {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 9999; /* Устанавливаем z-index больше, чем у родительского компонента, чтобы он был поверх него */
  padding: 20px;
  background-color: #fff;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.5);
}
.event-form-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.event-form-wrapper {
  background-color: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.5);
  display: flex;
  flex-direction: column;
}

.event-form {
  display: flex;
  flex-direction: column;
}

.form-group {
  display: flex;
  flex-direction: column;
  margin-bottom: 10px;
}

label {
  font-weight: bold;
  margin-bottom: 5px;
}

input[type="text"],
input[type="date"],
input[type="time"] {
  border: 1px solid black;
  border-radius: 5px;
  padding: 10px;
  font-size: 16px;
  margin-bottom: 5px;
}

button[type="submit"] {
  background-color: #008CBA;
  color: white;
  border: none;
  border-radius: 5px;
  padding: 10px;
  font-size: 16px;
  cursor: pointer;
}

.close-button {
  position: absolute;
  top: 10px;
  right: 10px;
  background-color: white;
  border: none;
  font-size: 20px;
  cursor: pointer;
  padding: 5px;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  display: flex;
}
</style>
