<script setup>
import { ref } from 'vue';

const showModal = ref(false) //set state for showing the "modal" textarea
const newNote = ref("")// state for the value of the textarea, as an empty string "2 way binding" via v-model
const notes = ref([])// state for the all the notes 

const getRandomColour = () => {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)"

}

const addNote = () => {
    if(newNote.value.length < 5) {return alert('task must have at least 5 letters')}
    notes.value.push({
    id: newNote.value.id,
    text: newNote.value,
    backgroundColor: getRandomColour()
  })
  showModal.value = false // hide textarea after added note
  newNote.value = "" // reset the textarea to empty after pressed add button
}


</script>


<template>
  <main>

    <div v-if="showModal" class="overlay">
      <div class="modal">

        <textarea v-model="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <button @click="addNote">Add Task</button>
        
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Bench Tasks Tracker</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="card-container">
        <div 
          v-for="note in notes" 
          :key="note.id"
          class="card" 
          :style="{ backgroundColor: note.backgroundColor }">
          <p class="main-text">{{ note.text }}
          
          <button>delete</button>
          </p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  height: 100vh;
  widows: 100vw;
  background-color: pink;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
  color: black;
}

header button {
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgb(41, 134, 83);
  border-radius: 100%;
  color: wheat;
  font-size: 20px;
  ;
}

.container {
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}

.card {
  width: 225px;
  height: 225px;
  background-color: goldenrod;
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;

}

.main-text {
  font-size: 35px;
  font-weight: bold;
  font-style: italic;
}

.date {

  font-size: 12.5px;
  font-weight: bold;
}

.card-container {
  display: flex;
  flex-wrap: wrap;
}

/* the delete card button */
.card-container button {
  border: solid;
  border-radius: 10px;
  padding: 20px;
  width: 100%;
  height: 20%;
  background-color:wheat;
  margin-top: 100px;
  font-style: oblique;
  font-weight: bolder;
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  /* background-color: rgba(0, 0, 0, 77); */
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  width: 750px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;

}

.modal button {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: wheat;
  border: none;
  color: black;
  cursor: pointer;
  margin-top: 15px;
}
</style>