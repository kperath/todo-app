<template>
  <div id="todo" class="flex flex-col items-center p-4 font-mono text-lg h-screen">
    <h1 class="uppercase bold text-blue-900 text-2xl p-2">TODO LIST
      <div class="float-right bg-blue-900 text-blue-500 lowercase px-2 ml-2 mt-1 rounded-full">
        <svg class="fill-current" xmlns="http://www.w3.org/2000/svg" height="25" viewBox="5 7 12 12" width="10"><path d="M0 0h24v24H0z" fill="none"/><path d="M9 16.2L4.8 12l-1.4 1.4L9 19 21 7l-1.4-1.4L9 16.2z"/></svg>
      </div>
    </h1>
    <div class="flex flex-col items-start">
      <div> <!-- div used to keep consistent width -->
          <div class="border-8 border-blue-900 mt-4 p-2 rounded-lg shadow-lg">
              <input @keyup.enter="addTask" class="p-2 capitalize rounded-sm" placeholder="Add Todo" maxlength="30" v-model="task">
              <button @click="addTask" class="capitalize bg-red-500 text-red-900 ml-2 px-2 py-3 rounded-lg">Add Todo</button>
          </div>
          <ul class="mt-2 rounded-lg">
              <li class="border-8 border-blue-800 bg-white p-2 mt-4 capitalize rounded-lg" v-for="(value, key) in tasks" :key="key">{{ value }}
                <!-- <button @click="removeTask(key)" class="float-right bg-red-500 text-red-900 lowercase px-2 ml-2 mb-2 rounded-sm">x</button> -->
                {{ key }}
                <button @click="removeTask(key)" class="float-right bg-red-500 text-red-900 lowercase px-2 ml-2 mb-2 rounded-full">
                  <svg class="fill-current" xmlns="http://www.w3.org/2000/svg" height="27" viewBox="5 7 12 12" width="11"><path d="M0 0h24v24H0z" fill="none"/><path d="M9 16.2L4.8 12l-1.4 1.4L9 19 21 7l-1.4-1.4L9 16.2z"/></svg>
                </button>
              </li>
          </ul>
          {{tasks}}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  data() {
    return {
      tasks: {},
      task: '', // change to include associated id so remove button works
      taskId: 0,
      whiteSpace : new RegExp("^\\s+$") // for whitespace detection in input field
    }
  },
  methods: {
    addTask : function() {
        if (this.task != '' && !this.whiteSpace.test(this.task)) {
            this.tasks[this.taskId++] = this.task;
        }
        this.task = ''; // reset text field
    },

    removeTask : function(key) {
        delete this.tasks[key]
        this.$forceUpdate(); // shows deletion immediately
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
