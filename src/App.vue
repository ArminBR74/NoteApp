<script setup>
import { ref } from "vue";
const showModal = ref(false);
const newNote = ref("");
const notes = ref([]);
const errorMessage = ref("");

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ",100%,75%)";
}
const addNotes = () => {
  if (newNote.value.length === 0) {
    return (errorMessage.value = "you cant add notes empty");
  }
  notes.value.push({
    id: Math.floor(Math.random() * 10000000),
    text: newNote.value,
    date: new Date(),
    background: getRandomColor(),
  }),
    (showModal.value = false),
    (newNote.value = ""),
    (errorMessage.value = "");
};
</script>
<template>
  <main>
    <div v-show="showModal" class="overlay">
      <div class="modal">
        <textarea
          name="note"
          id="note"
          cols="50"
          rows="10"
          v-model="newNote"
        ></textarea>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <button @click="addNotes">Add</button>
        <button class="close" @click="showModal = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header class="head">
        <h1 class="heading">Notes</h1>
        <button class="btn" @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div
          v-for="note in notes"
          :key="note.id"
          class="card"
          :style="{ background: note.background }"
        >
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("en-us") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  width: 1500px;
  height: 650px;

  margin: auto;
}
.container {
  width: 1000px;
  padding: 10px;
  margin: 0 auto;
}
.head {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.head > h1 {
  font-size: 3rem;
  font-weight: bold;
  color: #455a64;
  font-family: "Courier New", Courier, monospace;
}
.btn {
  border: none;
  width: 50px;
  height: 50px;
  border-radius: 200px;
  padding: 10px;
  background-color: rgb(0, 0, 0);
  color: #fff;
  cursor: pointer;
  font-size: 20px;
}

.card {
  width: 200px;
  height: 200px;
  background-color: rgb(26, 190, 116);
  border-radius: 11px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 10px;
  margin-bottom: 10px;
}
.main-text {
  margin-left: 10px;
}
.date {
  font-weight: bold;
  margin-left: 10px;
}
.cards-container {
  display: flex;
  flex-wrap: wrap;
}
.overlay {
  width: 100%;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
  position: absolute;
}

.modal {
  width: 600px;

  background-color: rgb(255, 255, 255);
  display: flex;
  padding: 30px;
  flex-direction: column;
  justify-content: center;

  border-radius: 15px;
}
.modal > textarea {
  background-color: #ececec;
  border: none;
  border-radius: 11px;
}
.modal > button {
  margin-top: 10px;
  padding: 10px 15px;
  background-color: #780865;
  border-radius: 11px;
  border: none;
  color: #fff;
  cursor: pointer;
  position: relative;
}
.modal .close {
  margin-top: 15px;
  background-color: chocolate;
}
.modal p {
  color: red;
}
</style>
