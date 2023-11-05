<script setup>
import { ref } from 'vue';
const inputChange = ref();
function addItem() {
  const table = document.querySelector('.table');
  const input = inputChange.value
  const newItem = document.createElement('div');
  newItem.classList.add('item');
  newItem.textContent = `${table.childElementCount + 1}. ${input}`;
  
  const maxWidth = table.clientWidth - newItem.clientWidth;
  const maxHeight = table.clientHeight - newItem.clientHeight;
  
  const randomX = Math.floor(Math.random() * (maxWidth - 50));
  const randomY = Math.floor(Math.random() * maxHeight);
  
  newItem.style.left = randomX + 'px';
  newItem.style.top = randomY + 'px';
  
  table.appendChild(newItem);
  inputChange.value = ''
}
</script>

<template>
  <div class="container-fluid">
      <div class="row">
        <div class="table">
          <div class="item">Item 1</div>
        </div>
        <div class="bottom">
          <input type="text" class="form-control input" placeholder="Enter YourName" @keyup.enter="addItem" v-model="inputChange">
          <button class="btn btn-outline-primary" @click="addItem">Thêm Mục</button>
        </div>
      </div>
    </div>
</template>
<style scoped>
.table {
  position: relative;
  width: 100%;
  min-height: 80vh;
  overflow: scroll;
}
.bottom{
  position: fixed;
  bottom: 10px;
  width: 100%;
  text-align: center;
}
button{
  min-width: 200px;
}
.flex{
  display: flex;
}
.input{
  max-width: 500px;
  margin: auto;
  margin-bottom: 5px;
}
</style>