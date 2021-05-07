<template>
  <section class="monthYear">
    {{currentNameMonth}} {{currentYear}}
  </section>
  <section class="days">
    <p class="day" v-for="day in days" :key="day">{{day}}</p>
  </section>
  <section class="dates">
    <!-- this iteration will give us the number of days in the month that we are in -->
    <p class="date" v-for="num in startDay()" :key="num"></p>
    <p class="date" v-for="num in daysInMonth()" :key="num">{{num}}</p>
  </section>
  <section class="toggleButtons">
    <button class="button" @click="prev">Prev</button>
    <button class="button" @click="next">Next</button>
  </section>
</template>

<script>

export default {
  data () {
    return {
      //this gives us the number of the month, we add one so that we can get the actual month and not the index
      currentMonth : new Date().getMonth(),
      // this gives us the year
      currentYear : new Date().getFullYear(),
      //days array
      days : ["Sun", "Mon" , "Tue", "Wed" , "Thurs" , "Fri" , "Sat"],
    }
  },
  methods: {
    //using this method we will get the number of days in the month
    daysInMonth() {
      return new Date(this.currentYear, this.currentMonth+1, 0).getDate();
    }, 
    startDay() {
      return new Date(this.currentYear, this.currentMonth , 1).getDay();
    }, 
    next() {
      if (this.currentMonth === 11 ) {
        this.currentYear++;
      }
      this.currentMonth++;
    },
    prev() {
      if (this.currentMonth === 0 ) {
        this.currentYear--;
      }
      this.currentMonth--;
    }
  },
  computed: {
    currentNameMonth() {
      return new Date(this.currentYear, this.currentMonth).toLocaleString("default", {month: "long"});
    }
  }
}
</script>

<style>

.monthYear {
  font-size: 40px;
  font-weight: bold;
  color: grey;
}

.days {
  display: flex;
  justify-content: center;
}

.day {
  padding: 10px;
  font-weight: bold;
  font-size: 30px;
  width: 14.28%;
}

.dates {
  display: flex;
  flex-wrap: wrap;
}

.date {
  width: 14.28%;
  text-align: center;
  justify-content: center;
}

.toggleButtons {
  display: flex;
  justify-content: space-between;

}

.button {
  border: black 1px solid;
  border-radius: 10px;
  font-size: 30px;
  margin: 30px;
  padding: 20px;
}

</style>