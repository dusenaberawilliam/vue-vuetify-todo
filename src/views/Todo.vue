<template>
  <div>
    <v-text-field
      class="pa-4"
      outlined
      label="add todo task"
      append-icon="mdi-plus"
      hide-details
      clearable
      v-model="taskTitle"
      @keyup.enter="addTask"
      @click:append="addTask"
    ></v-text-field>
    <v-alert
      color="grey lighten-2 black--text"
      dark
      dense
      v-if="tasks.length === 0"
      class="ma-4 pa-3"
    >
      No taks found
    </v-alert>
    <v-list class="pt-0" flat>
      <div v-for="task in tasks" :key="task.id">
        <v-list-item
          @click="didTask(task.id)"
          :class="{ 'blue lighten-5': task.done }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through': task.done }"
                >{{ task.title }}
              </v-list-item-title>
            </v-list-item-content>
            <v-list-item-action>
              <v-btn icon @click.stop="deleteTask(task.id)">
                <v-icon color="red lighten-1">mdi-delete</v-icon>
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
      taskTitle: "",
      tasks: [],
    };
  },
  methods: {
    didTask(id) {
      let task = this.tasks.filter((task) => task.id == id)[0];
      task.done = !task.done;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    addTask() {
      this.tasks.push({
        id: Date.now(),
        title: this.taskTitle,
        done: false,
      });
      this.taskTitle = "";
    },
  },
};
</script>
