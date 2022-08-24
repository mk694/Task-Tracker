<template>
  <form class="add-form" @submit="submitHandler">
    <div class="form-control">
      <label> Task </label>
      <input type="text" v-model="text" name="text" placeholder="Add Task" />
      <div class="error-txt" v-if="textErr">Please provide text!</div>
    </div>

    <div class="form-control">
      <label> Day & Time </label>
      <input
        type="date"
        name="day"
        v-model="day"
        placeholder="Add day and time"
      />
      <div class="error-txt" v-if="dayErr">Please provide date!</div>
    </div>
    <div class="form-control reminder">
      <label>Set Reminder</label>
      <input type="checkbox" v-model="reminder" />
    </div>
    <div class="button-wrapper">
      <button type="submit">Submit</button>
    </div>
  </form>
</template>

<script>
export default {
  name: "new-task-form",
  props: [],

  data() {
    return {
      text: "",
      day: "",
      reminder: false,
      textErr: false,
      dayErr: false,
    };
  },

  methods: {
    submitHandler(e) {
      e.preventDefault();

      const d = new Date(this.day);
      let day = d.getDay();
      let date = d.getDate();
      let m = d.getMonth();

      const days = [
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
        "Sunday",
      ];
      const months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];

      if (this.text === "") {
        this.textErr = true;
      }

      if (this.day === "") {
        this.dayErr = true;
      }

      if (this.text !== "" && this.day !== "") {
        const randomeID = Math.random() * 100000;

        const newTask = {
          id: randomeID,
          text: this.text,
          day: ` ${date} ${months[m]}, ${days[day]}`,
          reminder: this.reminder,
        };
        this.$emit("add-task", newTask);

        this.text = "";
        this.day = "";
        this.reminder = false;
        this.textErr = false;
        this.dayErr = false;
      }
    },
  },

  emits: ["add-task"],
};
</script>

<style lang="scss" scoped>
.error-txt {
  font-size: 10px;
  color: red;
  margin-left: 5px;
}

.add-form {
  margin-bottom: 15px;
}
.form-control {
  display: flex;
  flex-flow: column;
  justify-content: space-between;
  margin-bottom: 10px;

  &.reminder {
    align-items: center;
    flex-flow: row;
    justify-content: space-between;
    margin-right: 15px;

    label {
      margin-bottom: 0px;
    }
    input {
      width: 16px;
      height: 16px;
    }
  }

  label {
    margin-bottom: 5px;
  }

  input {
    padding: 5px 10px;
    border-radius: 5px;
    outline: none;
    border: 1px solid darkgray;
  }
}
.button-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;

  button {
    width: 100%;
    color: #fff;
    background: #000;
    padding: 10px;
    border-radius: 5px;
    font-size: 15px;
    cursor: pointer;
    &:active {
      transform: scale(0.98);
    }
  }
}
</style>
