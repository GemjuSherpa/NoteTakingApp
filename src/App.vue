<script setup>
  import {ref} from 'vue'

  const showModal = ref(false)

  const newNotes = ref("")
  const errorMessage = ref("")

  const notes = ref([])

  const addNote = ()=>{
    if (newNotes.value.length <=10){
      return errorMessage.value = "Note must be 10 characters long."
    }

    notes.value.push({
      id: Math.floor(Math.random()*10000),
      text: newNotes.value,
      date: new Date(),
      backgroundColor: getRandomColor()
    })

    showModal.value = false
    newNotes.value = ""
    errorMessage.value = ""
  }

  const getRandomColor = ()=>{
    return "hsl(" + Math.random()*360 + ", 100%, 75%"
  }



</script>

<template>
  <main>
    <div v-show="showModal" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newNotes" name="note" id="note" cols="30" rows="10"></textarea>
        <p v-if="errorMessage">{{errorMessage}}</p>
        <button @click="addNote">Add Notes</button>
        <button class="close" @click="showModal = !showModal">Close</button>
      </div>
    </div> 
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = !showModal">+</button>
      </header>
      <div class="cards-container">
        <div class="card" v-for="note in notes" :key="note.id" :style="{backgroundColor: note.backgroundColor}">
            <p class="main-text">{{note.text}}</p>
            <p class="date">{{note.date}}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
  main{
    height: 100vh;
    width: 100vw;
  }

  .container{
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
  }

  header{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  h1{
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
  }
  button{
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: rgb(21, 20, 20);
    border-radius: 100%;
    color: white;
    font-size: 20px;
  }

  .card{
    width: 225px;
    height: 225px;
    background-color: rgb(237, 180, 44);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 25px;
  }

  .date{
    font-size: 12.5px;
    font-weight: bold;
  }

  .cards-container{
    display: flex;
    flex-wrap: wrap;
  }

  .overlay{
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.77);
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .modal{
    width: 750px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }

  .modal button{
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: blueviolet;
    color: white;
    cursor: pointer;
    margin-top: 15px;
    border: none;
    border-radius: 0;

  }

  .modal .close{
    background-color: rgb(231, 24, 69);
  }

  .modal p{
    color: red;
  }
</style>
