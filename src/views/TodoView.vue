<template>
  <div class="pa-6">
    <v-text-field
      v-model="newTaskTitel"
      @click:append="addTask"
      @keyup.enter="addTask"
      class="pa-4"
      outlined
      label="add task"
      append-icon="mdi-plus"
      hide-details
      clearable
    ></v-text-field>
    <div class="pt-0">
      <v-list flat v-for="task in tasks" :key="task.id">
        <v-list-item
          @click="doneTask(task.id)"
          :class="{ 'blue lighten-5': task.done }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through': task.done }"
                >{{ task.titel }}</v-list-item-title
              >
            </v-list-item-content>
            <v-list-item-action>
              <v-btn @click.stop="deleteTask(task.id)" icon>
                <v-icon color="primary lighten-1">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </v-list>
    </div>
  </div>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      newTaskTitel: "",
      tasks: [
        // {
        //   id: 1,
        //   titel: "wake up",
        //   done: false,
        // },
        // {
        //   id: 2,
        //   titel: "read a book",
        //   done: false,
        // },
        // {
        //   id: 3,
        //   titel: "go to gym",
        //   done: false,
        // },
      ],
    };
  },
  methods: {
    doneTask(id) {
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.done = !task.done;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    addTask() {
      let newTask = {
        id: Date.now(),
        titel: this.newTaskTitel,
        done: false,
      };

      this.tasks.push(newTask);
      this.newTaskTitel = "";
    },
  },
};
</script>
