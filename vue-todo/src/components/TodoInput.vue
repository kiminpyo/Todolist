<template>
 <!--v-on:keyup.enter ==>엔터 눌렀을때 동작하는 것-->
    <div class="inputBox shadow">
        <input 
        type="text"
         v-model="newTodoItem" 
         v-on:keyup.enter="addTodo">
       <!--   <button v-on:click="addTodo">add</button> -->
         <span class="addContainer" v-on:click="addTodo" >
            <i class="fas fa-plus-square"></i>
         </span>
    </div>
</template>

<script>
export default {
    data: function () {
        return{
            newTodoItem: ""
        }
    },
    methods: {
        //여기에서의 this 는 input의 this다 
        addTodo : function(){ 
            if(this.newTodoItem !== ''){
                 var obj = {
                completed: false, 
                item: this.newTodoItem 
                };
            //저장하는 로직
            //json을 사용하면 storage에 있는 값들을 string으로 볼수있다. 그냥 obj넣으면 object로 떠버림
            /* localStorage.setItem(this.newTodoItem, obj); */
              localStorage.setItem(this.newTodoItem, JSON.stringify(obj));
               this.clearInput(); 
            }
        },
        clearInput: function(){
            this.newTodoItem = '';
        }
    }
}
</script>

<style scoped>
input:focus{
    outline:none;
}
.inputBox{
    background: white;
    height: 50px;
    line-height:50px;
    border-radius: 5px;
}
.inputBox input{
    border-style: none;
    font-size: 1.1rem; 
    text-align:start;
}
.addContainer{
    float: right;
    background: linear-gradient(to left, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}
.addBtn{
    color:white;
    vertical-align: middle;
}
</style>