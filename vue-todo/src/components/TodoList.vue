<template>
  <div>
      <ul>
        <!--todoite의 중복되지 않는 선에서 v
        index==vue의 장점== index를 써주면 list의 순서를 따라간다-->
        <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.item" class="shadow">
          <i class="checkBtn fas fa-check" 
            v-bind:class="{checkBtnCompleted: todoItem.completed}"
            v-on:click="toggleComplete(todoItem, index)"></i>
          <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
         <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
           <i class="fas fa-trash-alt"></i>
           </span>
        </li>
        
      </ul>
  </div>
</template>

<script>
  export default {
    data: function() {
      return{
        todoItems: []
      }
    },
    methods:{
      removeTodo: function(todoItem, index){
        console.log(todoItem,index)
        localStorage.removeItem(todoItem.item);
        // ["hi" , "hello" , "ddd" ] 에서 인덱스번호만큼 1개를 지우갰다. slice와 splice
        this.todoItems.splice(index, 1);
      },
      toggleComplete: function(todoItem, index){
        console.log(todoItem, index);
        todoItem.completed = !todoItem.completed;
        // 로컬 스토리지의 데이터를 갱신
        localStorage.removeItem(todoItem.item);
        localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
      }
    },
    //생성되는 시점에 로직이 생성된다.
    created: function(){
      if(localStorage.length > 0){
        for(var i = 0; i < localStorage.length; i++){
          if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
            this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
            /* this.todoItems.push(localStorage.key(i)); */
          }
        }
      }
    }      
  }
</script>

<style scoped>
ul{
  list-style-type: none;
  padding-left:0px;
  margin-top: 0;
  text-align: left;
}
li{
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.5rem;
  background: white;
  border-radius: 5px;
}
.checkBtn{
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.checkBtnCompleted{
  color: #b3adad;
}
.textCompleted{
  text-decoration: none;
  color: #b3adad;
}
.removeBtn{
  margin-left: auto;
  color: #de4343;
}
</style>