<template>
  <div id="todo" class="flex flex-col items-center p-4 font-mono text-lg h-screen">
    <h1 class="uppercase bold text-blue-900 text-2xl p-2">TODO LIST</h1>
            <div class="flex flex-col items-start">
            <div> <!-- div used to keep consistent width -->
                <div class="border-8 border-blue-900 mt-4 p-2 rounded-lg shadow-lg">
                    <input @keyup.enter="addItem" class="p-2 capitalize" placeholder="Add Item" maxlength="30" v-model="listItem">
                    <button @click="addItem" class="capitalize bg-red-500 text-red-900 ml-2 px-2 py-4 rounded-lg">Add Item</button>
                </div>
                <ul class="mt-2 rounded-lg">
                    <li class="border-8 border-blue-800 bg-white p-2 mt-4 capitalize rounded-lg" v-for="(value, key) in items" :key="key">{{ value }}<button @click="removeItem(key)" class="float-right bg-red-500 text-red-900 lowercase px-2 ml-2 mb-2 rounded-sm">x</button></li>
                </ul>
            </div>
        </div>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  data() {
    return {
      items: {},
      listItem: '', // change to include associated id so remove button works
      listId: 0,
      isEmpty: true,
      whiteSpace : new RegExp("^\\s+$") // for whitespace detection in input field
    }
  },
  methods: {
    addItem : function() {
        
        if (this.listItem != '' && !this.whiteSpace.test(this.listItem)) {
            this.items[this.listId++] = this.listItem;
        }
        this.listItem = ''; // reset text field
    },

    removeItem : function(key) {
        delete this.items[key]
        this.$forceUpdate(); // shows deletion immediately
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
