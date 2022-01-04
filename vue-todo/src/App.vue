<template>
  <div id="app">
    <!--태그 방식에 대해서 스타일 관리를 가져라 꼭-->
  
  <TodoHeader></TodoHeader>
  
  <TodoInput v-on:addTodoItem="addOneItem"></TodoInput>
  
  <TodoList
    v-bind:propsdata="todoItems"
    v-on:removeItem="removeOneItem"
    v-on:toggleItem="toggleOneItem">
  </TodoList>
  
  <TodoFooter v-on:clearAll="clearAllItems"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  
  data: function(){
        return{
          todoItems: []
        }
      },
  methods:{
    addOneItem: function(todoItem){
                var obj = {
                completed: false, item: todoItem};
                localStorage.setItem(todoItem, JSON.stringify(obj));
                this.todoItems.push(obj);
        },
    removeOneItem: function(todoItem, index){
      localStorage.removeItem(todoItem.item);
        // ["hi" , "hello" , "ddd" ] 에서 인덱스번호만큼 1개를 지우갰다. slice와 splice
        this.todoItems.splice(index, 1);
    },
    toggleOneItem: function(){
        this.todoItems[index].completed = !this.todoItems[index].completed;
        // 로컬 스토리지의 데이터를 갱신
        localStorage.removeItem(todoItem.item);
        localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    clearAllItems: function(){
      localStorage.clear();
      this.todoItems = [];
    }
  },
  created: function() {
      if (localStorage.length > 0) {
        for(var i = 0; i < localStorage.length; i++){
          if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
            this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
            /* this.todoItems.push(localStorage.key(i)); */
          }
        }
      }      
    },
   components: {
     //컴포넌트 태그명: 컴포넌트 내용
     'TodoHeader' : TodoHeader,
     'TodoInput' : TodoInput,
     'TodoList' : TodoList,
     'TodoFooter' : TodoFooter
   }
   
}
</script>

<style>
body{
  text-align: center;
  background-color: #F6F6F6;
}
input{
  border-style: groove;
  width: 200px;  
}
button{
  border-style: groove;
}
/* 박스에 그림자 주는 효과 */
.shadow{
  box-shadow: 50px 10px 10px rgba(0,0,0,0.03);
}
</style>
