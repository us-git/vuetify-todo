<template>
  <div class="home">
      <v-text-field
      v-model="newTaskTitle"
      outlined
      label="Add task"
      append-icon="mdi-plus"
      class="pa-3"
      hide-details
      clearable
      @click:append="addTask"
      @keyup.enter="addTask"
  >
  </v-text-field>
    <v-list 
      flat
      class="pt-0"
      v-if="tasks.length"
    >
  

    <div v-for="task in tasks" :key="task.id" >
      <v-list-item @click="doneTask(task.id)" :class="{ 'orange lighten-5' : task.done }">
          <template>
          <!-- <template v-slot:default="{ active, }"> -->
            <v-list-item-action>
              <v-checkbox
                :input-value="task.done"
                color="primary"
              ></v-checkbox>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title :class="{ 'text-decoration-line-through' : task.done }">{{ task.title }}</v-list-item-title>
            </v-list-item-content>

            <v-list-item-action>
          <v-btn icon @click.stop="deleteTask(task.id)">
            <v-icon color="primary lighten-1">mdi-delete</v-icon>
          </v-btn>
        </v-list-item-action>
          </template>

          
      </v-list-item>
      
        </v-list-item>
        <v-divider></v-divider>
    </div>
</v-list>
    <div v-else class="no-tasks">
      <v-icon
        size="100px"
        color="primary"
      >mdi-check</v-icon>
      <div class="text-h5 primary--text">No tasks</div>
    </div>
        
    
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      newTaskTitle: "Add task",
      tasks: [
        {
          id: 1,
          title: "Wake up",
          done: false,
        },
        {
          id: 2,
          title: "Get bananas",
          done: false,
        },
      ],
    };
  },
  methods: {
    addTask() {
      let newTask = {
        id: Date.now(),
        title: this.newTaskTitle,
        done: false,
      };
      this.tasks.push(newTask);
      this.newTaskTitle = "";
    },
    doneTask(id) {
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.done = !task.done;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
  },
};
</script>

<style lang="sass">
  .no-tasks
    position: absolute
    left: 50%
    top: 50%
    transform: translate(-50%, -50%)
    opacity: 0.5
</style>
