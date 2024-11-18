<script setup>

import {reactive, ref, computed} from 'vue';



const  todo = ref("")



const addTodo = () => {
  if(todo.value === ''){
    return
  }
}

todos.push({
  id: todos.length + 1,
  title: todos.value,
  id: false

})

// todo.value = "";

const todos = reactive([
  {
    id: 1,
    title: 'Todo One',
    completed: false
  },
  {
    id: 2,
    title: 'Todo Two',
    completed: false
  }, 
  {
    id: 3,
    title: 'Todo Three',
    completed: true
  },

])

// const addTodo = () => {
//   // console.log('add');
// }



const checkComplete = (index) => {
    todos[index].completed = !todos[index].completed
}

const removeTodo = (index) => {
    todos.splice(index, 1)

}

const countAllTodo = computed(() => {
  return todos.length
})

const countCompleteTodo = computed(() => {
  return todos.filter(todo => todo.completed).length
})



</script>



<template>
    <div class="max-w-md mx-auto bg-white shadow-lg rounded-lg overflow-hidden mt-16 border p-6 space-y-6">
        <h1 class="text-2xl uppercase text-gray-700 font-bold">To Do List <span v-if="todos.length"> ({{ countCompleteTodo }}/{{ countAllTodo }}) </span> </h1>

        <!-- {{ todos }} -->

        <form action="" @submit.prevent="addTodo" >
          <div class="flex items-center border-b-2 border-teal-500 py-2">
            <input v-model="todo" class="border-none focus:outline-none w-full" type="text" placeholder="Add a task">
            <button class="flex-shrink-0 bg-teal-500 hover:bg-teal-700 text-white py-1 px-2" type="submit">Add</button>
          </div>
        </form>


        <ul v-if="todos.length">
          <li v-for="(todo, index) in todos" :key="todo.id">
            <div class="flex items-center justify-between">
              <div class="flex items-center">
                  <input @input="checkComplete(index)" :checked="todo.completed" class="h-4 w-4 text-teal-500 focus:ring-teal-500 border-gray-300 rounded" type="checkbox" name="todo" id="`todo-${todo.id}`"> 
                  <label for="todo" class="ml-3 block text-gray-900 " :class="{'line-through' : todo.completed}">
                    <span class="text-lg font-medium">{{ todo.title }}</span>
                  </label>
              </div>

              <button @click="removeTodo(index)" class="flex-shrink-0 ">
                Delete
              </button>
            </div>
          </li>

        </ul>

        <div v-else>
          <p>No tasks yet.</p>
        </div>
        


    </div>
</template>



<style scoped>

</style>
