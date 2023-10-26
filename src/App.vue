<template>
 <div class="wrapper">
  <h1>TO DO LIST</h1>
 <div>
 <form  class="inputField" @submit.prevent="create">
 <input  v-model="newTodo" autocomplete="off">
 <button type="submit">ADD TASK</button>
</form>
</div>
<ul class="todooList">
  <li v-for="item in todos" :key="item.id">
    
    <h3 :class="{done : item.completed}" @click="completed(item)">{{ item.content }}</h3>
    <button class="remove" @click="remove(item)">REMOVE</button>
  </li>
</ul>
<div class="footer">
  <button  @click="markAll">SELECT ALL</button>
</div>
</div>
</template>

<script>
 import { ref } from 'vue'
export default{
  setup(){
    const todos = ref([])
    const newTodo = ref('')
    function create(){
      todos.value.push({
        id:Date.now(),
      content:newTodo.value, 
      completed:false
          })
          newTodo.value=''
    }
    function remove(item){
        todos.value.splice(todos.value.indexOf(item),1)
    }
    function completed(item){
      item.completed=!item.completed
    }
    function markAll(){
     todos.value.forEach((todo)=> todo.completed=true)
    }
    return{
      todos,
      newTodo,
      create,
      remove,
      completed,
      markAll
    }
  }
}

</script>

<style>
*{
  margin: 0;
  padding: 0;
  font-family: 'poppins' , sans-serif;
}

h1{
    font-size: 20px;
    line-height: 32px;
    margin: 0 0 12px 0;
    color: #272727;
}  
body{
width: 100%;
height:100vh ;
padding: 10px;
background: rgb(238,174,202);
background: -moz-radial-gradient(circle, rgba(238,174,202,1) 0%, rgba(148,187,233,1) 100%);
background: -webkit-radial-gradient(circle, rgba(238,174,202,1) 0%, rgba(148,187,233,1) 100%);
background: radial-gradient(circle, rgba(238,174,202,1) 0%, rgba(148,187,233,1) 100%);
filter: progid:DXImageTransform.Microsoft.gradient(startColorstr="#eeaeca",endColorstr="#94bbe9",GradientType=1);
}
.wrapper{
  background-color: rgba(116, 75, 75, 0.3);
  color: #222;
  max-width:400px ;
  width: 100%;
  margin: 120px auto;
  padding: 25px;
  border-radius: 5px;
  box-shadow: 0px 10px 15px rgba(0, 0, 0, 0.1);
  
}
input {
  width: 100%;
  display: inline-block;
  margin: 8px 0 ;
  height: 100%;
  border-radius: 4px;
  border: 1px solid #ccc;
  box-sizing: border-box;
  font-size: 17px;
  padding: 12px 20px;
  transition: all 0.2s ease;
}
form button{
  width:100% ;
  height: 100%;
  border: none;
  color: #fff;
  margin-left:5px ;
  font-size: 21px;
  outline: none;
  background: #454548;
  cursor: pointer;
  border-radius: 3px;
  pointer-events: none;
  transition: all 0.2 ease;
}
.wrapper .todoList{
  margin-top: 50px;
  max-height: 400px;
  overflow-y: auto;
}
li{
  position: relative;
  list-style: none;
  margin-bottom: 8px;
  margin-top: 8px;
  background: #d3d3d3;
  border-radius: 3px;
  padding: 10px 15px;
  cursor: default ;
  overflow: hidden;
  word-wrap: break-word;
}
.footer{
  display: flex;
  width: 100%;
  margin-top: 20px;
  align-items: center;
  justify-content: space-between;
}
.footer button{
padding: 6px 10x;
border-radius: border-box;
border: 50px;
color: #fff;
background: #426e52;
cursor: pointer;

width: 80px;
 height: 40px;
    
    
}
.remove{
  margin-left: auto; 
}

.done{
  text-decoration: line-through;
}
.item{
  cursor: pointer;
}
</style>
