<script setup>
import { ref,onMounted } from 'vue';
const inputChange = ref("");
const domainCurrent = "https://vinhcity.net/api.php?"
const keyword = ref("")
function addItem(input) {
  // if(inputChange.value.length < 2){
  //   alert("Input Empty")
  //   return
  // }
  const table = document.querySelector('.table');
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
const reload = async () =>{
    var requestOptions = {
    method: 'GET',
    redirect: 'follow'
  };
  var response = await fetch(`${domainCurrent}get=&token=${keyword.value}`, requestOptions);
  var res = await response.json()
  res.forEach(element => {
    addItem(element.username)
  });
}
const addItemDatabase = async () =>{
    var requestOptions = {
    method: 'GET',
    redirect: 'follow'
  };
  var response = await fetch(`${domainCurrent}username=`+inputChange.value+`&token=${keyword.value}`, requestOptions);
  var res = await response.json()
  addItem(inputChange.value)
}
onMounted(()=>{
  reload()
  keyword.value = localStorage.getItem('key')
})
</script>

<template>
  <div class="container-fluid">
      <div class="row">
        <div class="table">
          
        </div>
        <div class="bottom">
          <input type="text" class="form-control input" placeholder="Enter YourName" @keyup.enter="addItemDatabase" v-model="inputChange">
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