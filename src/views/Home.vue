<template>
<div class="home">
  <v-text-field label="Add Task" class="pa-3" append-icon="mdi-plus" outlined hide-details clearable v-model="newTask" @click:append="addTask" @keyup.enter="addTask"></v-text-field>
  <v-list two-line flat app class="pt-0">
    <div v-for="task in tasks" :key="task.id">

      <v-list-item @click="doneTask(task.id)" :class="{'blue lighten-5': task.done}">
        <template v-slot:default>
          <v-list-item-action>
            <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
          </v-list-item-action>

          <v-list-item-content>
            <v-list-item-title :class="{'text-decoration-line-through': task.done}">{{task.title}}</v-list-item-title>
          </v-list-item-content>
          <v-list-item-action>
            <v-btn icon @click.stop="deleteTask(task.id)">
              <v-icon color="primary lighten-1">mdi-delete</v-icon>
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
  name: 'Home',
  data() {
    return {
      newTask: '',
      tasks: [{
          id: 1,
          title: 'Take out the Trash',
          done: false,
        },
        {
          id: 2,
          title: 'Wake up early',
          done: false,
        },
        {
          id: 3,
          title: 'Code today',
          done: false,
        }
      ],
      createdAt: '',
    }
  },
  methods: {
    doneTask(id) {
      let [task] = this.tasks.filter(task => task.id === id);
      task.done = !task.done;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter(task => task.id !== id)
    },
    addTask(){
      const newTask = {
        title: this.newTask,
        id: Date.now(),
        done: false
      }
      this.tasks.push(newTask);
      this.newTask = '';
    }
  },
}
</script>
