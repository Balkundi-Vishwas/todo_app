<template>
  <div class="container" style="max-width: 600px">
    <h2 class="text-center mt-5">Todo App</h2>

    <div class="d-flex mt-5">
      <input type="text" v-model="task" placeholder="Enter task" class="w-100 form-control" />
      <button class="btn btn-success rounded-2" @click="submitTask">
        SUBMIT
      </button>
    </div>

    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col" style="width: 120px">Status</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks">
          <td>
            <span>
              {{ task.name }}
            </span>
          </td>
          <td>
            <span class="btn btn-warning pointer" @click="changeStatus(index)">
              {{ capitalizeFirstChar(task.status) }}
            </span>
          </td>
          <td class="text-center">
            <div @click="deleteTask(index)">
              <span class="btn btn-danger rounded-2 pointer">Delete</span>
            </div>
          </td>
          <td class="text-center">
            <div>
              <p class="btn btn-primary rounded-2 pointer">Edit</p>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },

  data() {
    return {
      task: "",
      editedTask: null,
      statuses: ["to-do", "in-progress", "finished"],
      tasks: [
        {
          name: "Steal bananas from the supermarket.",
          status: "to-do",
        },
      ],
    };
  },

  methods: {
    /**
     * Capitalize first character
     */
    capitalizeFirstChar(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },

    changeStatus(index) {
      let newIndex = this.statuses.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.statuses[newIndex];
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },

    submitTask() {
      if (this.task.length === 0) return;
      else {
        this.tasks.push({
          name: this.task,
          status: "to-do",
        });
      }

      this.task = "";
    },
  },
};
</script>

<style scoped>
.pointer {
  cursor: pointer;
}
</style>