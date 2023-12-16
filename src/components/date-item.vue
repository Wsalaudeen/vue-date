<template>
  <h1>Date: {{ currentDate }}</h1>
  <h1>Day: {{ day }}</h1>
  <h1>Month: {{ month }}</h1>

  <form @submit.prevent="AddDate">
    <div>
      <label for="day"> Day: </label>
      <input
        type="number"
        name="day"
        placeholder="Enter day..."
        v-model="dateobj.day"
      />
    </div>

    <div>
      <label for="month"> Month: </label>
      <input
        type="number"
        name="month"
        id=""
        placeholder="Enter month..."
        v-model="dateobj.month"
      />
    </div>
    <div>
      <label for="year">
        Year:
      </label>
      <input type="number" name="year" id="" placeholder="Enter year..." v-model="dateobj.year">
    </div>
    
    <button>Get Day</button>
  </form>

  <p>{{ customDate }}</p>
</template>

<script>
import { onMounted, ref } from "vue";
import useDate from "../custom-hooks/useDate";

export default {
  setup() {
    const { date, getDay, getMonth, createCustomDate } = useDate();

    let day = ref(null);
    let month = ref(null);
    let currentDate = ref(null);
    let customDate = ref(null);
    let dateobj = ref({
      day: null,
      month: null,
      year: null
    });

    onMounted(() => {
      currentDate.value = date.toString();
      day.value = getDay();
      month.value = getMonth();
    });

    function AddDate() {
      customDate.value = createCustomDate(
        dateobj.value.year,
        dateobj.value.month,
        dateobj.value.day
      );
    }

    return { currentDate, day, month, customDate, AddDate, dateobj };
  },
};
</script>

<style>
form {
  max-width: 400px;
  margin: 10px auto;
  height: 180px;
  padding: 8px;
  text-size-adjust: 1.5em;
  font-weight: 600;
  background-color: red;
  border-radius: 8px;
  
}

form > div {
  display: flex;
  margin: 10px auto;
  justify-content: space-around;
  text-align: left;
}

input {
  padding: 8px;
  width: 60%;
  border-radius: 6px;
  border: none;
}

button {
  margin-top: 12.5px;
  padding: 10px 20px;
  border-radius: 5px;
  border: none;
  cursor: pointer;
  outline-offset: none;
}
 button:hover{
  color: white;
  background-color: black;
 }
</style>
