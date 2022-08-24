<template>
  <div class="tasks-wrapper">
    <div class="tasks-container">
      <Header title="Task tracker" />
      <Form @add-task="addTask" />

      <Tasks
        @toggle-reminder="toggleReminder"
        @remove-task="deleteTask"
        :tasks="tasks"
      />
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Tasks from "./components/Tasks.vue";
import Form from "./components/Form.vue";
export default {
  name: "App",
  components: { Header, Tasks, Form },

  methods: {
    addTask(newtask) {
      console.log(this.tasks);

      return (this.tasks = [...this.tasks, newtask]);
    },

    deleteTask(id) {
      setTimeout(
        () => {
          if (confirm("Are you sure?")) {
            this.tasks = this.tasks.filter((task) => {
              return task.id !== id;
            });
          }
        },

        100
      );
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) => {
        if (task.id === id) {
          const newReminder = !task.reminder;

          return {
            ...task,
            reminder: newReminder,
          };
        }
        return task;
      });
    },
  },
  emits: ["remove-task", "toggle-reminder", "submit-form"],

  data() {
    return {
      tasks: [],
    };
  },

  created() {
    this.tasks = [
      {
        id: 1,
        text: "Dentist Appointment",
        day: "25 August, Thursday",
        reminder: true,
      },
      {
        id: 2,
        text: "Gym session",
        day: "24 August, Wednesday",
        reminder: true,
      },
      {
        id: 3,
        text: "Tennis  Practice",
        day: "27 August, Saturday",
        reminder: false,
      },
    ];
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
}

.tasks-wrapper {
  min-width: 305px;
  max-width: 500px;
  margin: 15px auto;
  display: flex;
  align-items: center;
  justify-content: center;
}

.tasks-container {
  padding: 15px;
  border: 1px solid steelblue;
  width: 100%;
  margin: 15px;
  header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 15px;
  }
}
</style>
