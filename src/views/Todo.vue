<template>
  <div class="todo">
    <v-text-field
      v-model="newTaskTitle"
      outlined
      label="Add Task"
      append-icon="mdi-plus"
      @click:append="addTask"
      @keydown.enter="addTask"
      class="mx-6 mt-6"
      clearable
      :error-messages="errorMessage"
    ></v-text-field>

    <v-list flat class="pt-0">
      <div v-for="task in tasks" :key="task.id">
        <v-list-item
          @click="doneTask(task.id)"
          :class="{ 'deep-purple lighten-5': task.done }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through': task.done }"
              >
                {{ task.title }}
              </v-list-item-title>
            </v-list-item-content>

            <v-list-item-action>
              <v-btn icon @click.stop @click="deleteTask(task.id)">
                <v-icon color="error">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      newTaskTitle: "",
      errorMessage: "",
      tasks: [
        {
          id: 1,
          title: "Wake up",
          done: false,
        },
        {
          id: 2,
          title: "Buy foods",
          done: false,
        },
        {
          id: 3,
          title: "Eat foods",
          done: false,
        },
      ],
      rules: {
        required: (value) => !!value || "Required.",
      },
    };
  },
  methods: {
    validate() {
      if (!this.newTaskTitle) {
        this.errorMessage = "Required";
        return false;
      }
      this.errorMessage = "";
      return true;
    },
    addTask() {
      console.log("addTask");
      if (!this.validate()) {
        return;
      }
      let newTask = {
        id: Date.now(),
        title: this.newTaskTitle,
        done: false,
      };
      this.tasks.push(newTask);
      this.newTaskTitle = "";
    },
    doneTask(id) {
      console.log("doneTask");
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.done = !task.done;
    },
    deleteTask(id) {
      console.log("deleteTask");
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    log(message) {
      console.log(message);
    },
  },
};
</script>
