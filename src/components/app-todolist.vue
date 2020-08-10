<template>
  <div>
    <div class="newTask">
      <input type="text" placeholder="Task..." id="taskInput" />
      <button name="add" @click="addTask">Add Task</button>
      <button name="clear" @click="this.taskInput.value = ''">
        Clear Input
      </button>
    </div>
    <div class="pageTab">
      <p @click="ToDoListShow = false" :class="{ not_active: ToDoListShow }">
        Not Completed
      </p>
      <p @click="ToDoListShow = true" :class="{ not_active: !ToDoListShow }">
        Completed
      </p>
    </div>
    <ul>
      <li>
        <div
          class="pageTask"
          v-for="task in filter"
          :key="task"
          @click="task.completed = !task.completed"
        >
          <p>{{ task.title }}</p>
          <ion-icon name="checkmark-outline" v-show="task.completed"></ion-icon>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    ToDoList: {
      required: true,
    },
    ToDoListShow: {
      required: true,
    },
  },
  methods: {
    addTask: function() {
      let input = document.getElementById("taskInput");
      if (input.value != "") {
        this.ToDoList.unshift({
          title: input.value,
          doneTask: false,
        });
      }
      input.value = "";
    },
    completed: function(task) {
      task.completed = !task.completed;
    },
  },
  computed: {
    filter() {
      if (this.ToDoList != null) {
        if (this.ToDoListShow == false) {
          return this.ToDoList.filter((t) => !t.completed);
        }

        if (this.ToDoListShow == true) {
          return this.ToDoList.filter((t) => t.completed);
        }
      }
    },
  },
};
</script>
