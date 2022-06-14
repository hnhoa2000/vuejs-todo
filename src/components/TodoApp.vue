<template>
  <div class="container">
    <h2 class="text-center mt-5">My Todo App</h2>

    <!--input-->
    <div class="d-flex">
      <input v-model="task" type="text" placeholder="Enter task" class="form-control">
      <button @click="submitTask" class="btn btn-warning rounded-0">Submit</button>
    </div>

    <!--Task table-->
    <table class="table table-bordered">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>
            <span :class="{ 'finished': task.status === 'finished' }">{{ task.name }}</span>
          </td>
          <td style="width:120px"><span class="pointer" @click="changeStatus(index)">{{ task.status }}</span></td>
          <td>
            <div class="text-center">
              <span class="pointer" @click="editTask(index)">Edit</span>
            </div>
          </td>
          <td>
            <div class="text-center">
              <span class="pointer" @click="deleteTask(index)">Delete</span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },

  data() {
    return {
      task: '',
      editedTask: null,
      availableStatuses: ['to-do', 'in-progress', 'finished'],
      tasks: [
        {
          name: 'task 1',
          status: 'to-do'
        }, {
          name: 'task 2',
          status: 'in-progress'
        }
      ]
    }
  },

  methods: {
    submitTask() {
      if (this.task.length === 0) {
        return;
      }
      if (this.editedTask === null) {
        this.tasks.push({
          name: this.task,
          status: 'to-do'
        })
      } else {
        this.tasks[this.editedTask].name = this.task;
        this.editTask = null;
      }
    },

    deleteTask(index) {
      this.tasks.splice(index, 1);
    },

    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

    changeStatus(index) {
      console.log(index);
      console.log(this.tasks);
      let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
      console.log(newIndex);
      if (++newIndex > 2) {
        newIndex = 0;
      }
      console.log(newIndex);
      this.tasks[index].status = this.availableStatuses[newIndex];
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pointer {
  cursor: pointer;
}

.finished {
  text-decoration: line-through;
}
</style>
