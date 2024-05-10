<template>
  <div class="container" style="max-width: 600px">
    <h1 class="text-center m-5">Todo App</h1>
    <div   class="d-flex">
        <h5 v-show ="isVisible">you are now editting task no : {{ tno + 1 }}</h5>
    </div>
    <div class="d-flex">
      <input type="text" v-model="task" placeholder="Enter task" class="w-100 form-control" />
      <button class="btn btn-success rounded-2" @click="submitTask">
        SUBMIT
      </button>
    </div>

    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">s.no</th>
          <th scope="col">Task</th>
          <th scope="col" style="width: 120px">Status</th>
          <th scope="col" class="text-center">Delete</th>
          <th scope="col" class="text-center">Edit</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>
            <span>{{ index+1 }}</span>
          </td>
          <td>
            <span :class="{ 'text-decoration: line-through': task.status === 'finished' }">
              {{ task.name }}
            </span>
          </td>
          <td>
            <!-- <span class="btn btn-warning pointer" @click="changeStatus(index)">
              {{ capitalizeFirstChar(task.status) }}
            </span> -->
            <div id="app">
              <div class="dropdown">
                <button class="dropbtn" :style="{ backgroundColor: bgColor(index) }" @click="toggleDropdown(index)">{{ task.status }}</button>
                <div class="dropdown-content" v-show="isOpen">
                  <a href="#" @click="selectItem(status, index)"  v-for="status in statuses">{{ status }}</a>
                </div>
              </div>
            </div>
          </td>
          <td class="text-center">
            <div @click="deleteTask(index)">
              <span class="fa fa-trash pointer"></span>
            </div>
          </td>
          <td class="text-center">
            <div @click="editTask(index)">
              <span class="fa fa-pen pointer"></span>
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
      isVisible: false,
      isOpen: false, // Flag to control dropdown visibility
      // bgColor:'blue'
      tno : 0,
      statuses: ["to-do", "in-progress", "finished"],
      tasks: [
        {
          name: "complete the homework within the specified time.",
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
    toggleDropdown(index) {
      this.isOpen = !this.isOpen;
    },
    // Update selected item and close dropdown
    selectItem(item, index) {
      this.selected = item;
      this.tasks[index].status = item
      this.isOpen = false; // Close dropdown after selecting an item
    },
    bgColor(index){
      if(this.tasks[index].status === 'to-do')
      return 'blue'
      else if(this.tasks[index].status === 'in-progress')
      return 'red'
      else
      return'green'
    },
    editTask(index) {
      this.task = this.tasks[index].name
      this.editedTask = index
      this.isVisible = !this.isVisible;
      this.tno = index
    },

    changeStatus(index) {
      let newIndex = this.statuses.indexOf(this.tasks[index].status);
      if (++newIndex > 2)
        alert("cannot change the status after finished");
      // newIndex=0
      else {
        this.tasks[index].status = this.statuses[newIndex];
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },

    submitTask() {
      if (this.task.length === 0) return;
      else if (this.editedTask != null) {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
        this.isVisible = !this.isVisible;
      }
      else {
        this.tasks.push({
          name: this.task,
          status: "to-do",
        });
      }

      this.task = "";
      // tno=this.index;
    },
  },
};
</script>

<style scoped>
.pointer {
  cursor: pointer;
}

.edit-this {
  text-decoration: line-through
}

.line-through {
  text-decoration: line-through
}

.dropbtn {
  /* background-color: #4CAF50; */
  color: white;
  padding: 2px 8px;
  font-size: 16px;
  border: none;
  cursor: pointer;
  border-radius: 8%;
}

/* Dropdown button on hover & focus */
.dropbtn:hover,
.dropbtn:focus {
  background-color: #3e8e41;
}

/* The container <div> - needed to position the dropdown content */
.dropdown {
  position: relative;
  display: inline-block;
}

/* Dropdown content (hidden by default) */
.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f9f9f9;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  z-index: 1;
}

/* Links inside the dropdown */
.dropdown-content a {
  color: black;
  padding: 12px 12px;
  text-decoration: none;
  display: block;
}

/* Change color of dropdown links on hover */
.dropdown-content a:hover {
  background-color: #ddd;
}

/* Show the dropdown menu on hover */
.dropdown:hover .dropdown-content {
  display: block;
}

/* Change the background color of the dropdown button when the dropdown content is shown */
.dropdown:hover .dropbtn {
  background-color: #3e8e41;
}
</style>