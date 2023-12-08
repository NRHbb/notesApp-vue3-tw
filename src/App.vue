<template>
  <main class="h-screen w-screen bg-gray-800">
    <div id="overlay" class="absolute w-full h-full  bg-[rgb(0,0,0,0.77)] z-10 flex items-center justify-center"
    v-if="modal"
    >
      <div id="modal" class="
      w-[700px] bg-white rounded-lg p-[30px] relative flex flex-wrap flex-col
      ">
        <textarea v-model.trim="newNote" name="noted" id="noted" cols="30" rows="10" class="border-4 hover:border-yellow-400 p-2.5"></textarea>
        <p v-if="errorMsg"
        class="text-red-500 font-semibold text-md"
        >{{ errorMsg }}</p>
        
        <button class="p-2.5 text-xl w-full bg-yellow-400 rounded-lg mt-4 font-semibold text-white cursor-pointer"
        @click="addNote"
        >
          Add Notes
        </button>
        <button class="p-2.5 text-xl w-full bg-orange-400 rounded-lg mt-4 font-semibold text-white cursor-pointer"
        @click="modal = false"
        >Close</button>
      </div>
    </div>
    <div id="container" class="max-w-[1000px] p-2.5 my-0 mx-auto">
      <header class="flex justify-between mt-5 mb-8 items-center ">
        <h1 class="text-5xl font-bold drop-shadow-xl mb-[25px]  text-yellow-400">notesApp</h1>
        <button class=" w-11 h-11  cursor-pointer rounded-full bg-[rgb(21,20,20)]
        "
        @click="modal = true"
        >
          <span class="text-3xl text-white font-bold text-center hover:text-yellow-400">+</span>
        </button>
      </header>
      <div id="card-container" class="flex flex-wrap sm:justify-center lg:justify-normal xl:justify-normal"
      
      > 
        <div id="card-notes" class="
        w-[200px] h-[200px] bg-orange-500 rounded-2xl
        flex justify-between p-2.5 flex-col mr-5 mb-5
        "
        v-for="note in notes"
        :key="note.id"
        :style="{ backgroundColor: note.backgroundColor }"
        >
          <p id="main-text">{{ note.text }}</p>
          <p id="date" class="font-bold text-[12.5px] text-end">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref } from 'vue';


const modal = ref(false)
const newNote = ref("")
const errorMsg = ref("")
const notes = ref([])


//create function to random notes color
function randomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

//create fungction to add new Notes
const addNote = () => {
  //create an error msg if new note is less than 10 characters
  if(newNote.value.length <10) {
    return errorMsg.value = "Notes must be at least 10 characters long!"
  }
  //create a logic to push new notes to notes array
  notes.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: randomColor()
  })
  modal.value = false
  newNote.value = ""
  errorMsg.value = ""
}

</script>

<style lang="scss" scoped>

</style>