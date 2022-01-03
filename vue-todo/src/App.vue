<template>
  <div id="app">
    <!--태그 방식에 대해서 스타일 관리를 가져라 꼭-->
  <TodoHeader></TodoHeader>
  <TodoInput></TodoInput>
  <TodoList></TodoList>
  <TodoFooter></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

/* var my_cmp = {
  template: '<div>my component</div>'
}
new Vue({
  el: '',
  components: {
    'my-cmp': my_cmp
  }
}) */
export default {
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
