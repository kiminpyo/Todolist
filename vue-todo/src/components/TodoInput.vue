<template>
 <!--v-on:keyup.enter ==>엔터 눌렀을때 동작하는 것-->
    <div class="inputBox shadow">
        <input 
        type="text"
         v-model="newTodoItem" 
         v-on:keyup.enter="addTodo">
         <span class="addContainer" v-on:click="addTodo" >
            <i class="fas fa-plus-square"></i>
         </span>
    <Modal v-if="showModal" @close="showModal = false">
        <!--slot은 현재 컴포넌트에서 재사용을 할 수 있다 modal에서 header만 끌어온것-->
            <h3 slot="header">
                경고!
               <span><i class="fas fa-times" @click="showModal = false"></i></span>
            </h3>
            <h3 slot="body">
               뭔가를 입력하세요
            </h3>
            <h3 slot="footer">
                copyright
            </h3>
    </Modal>
    </div>
</template>

<script>
import Modal from'./common/Modal.vue'

export default {
    data: function () {
        return{
            newTodoItem: "",
            showModal: false
        }
    },
    methods: {
        //여기에서의 this 는 input의 this다 
        //저장하는 로직
            //json을 사용하면 storage에 있는 값들을 string으로 볼수있다. 그냥 obj넣으면 object로 떠버림
            /* localStorage.setItem(this.newTodoItem, obj); */
        addTodo : function(){ 
            if(this.newTodoItem !== ''){
                //하위에서 발생한 이벤트를 this안의 인자로 값을 발생시켜 넘긴다
                this.$emit('addTodoItem', this.newTodoItem)
                this.clearInput(); 
            }else{
                this.showModal = !this.showModal;
            }
        },
        clearInput: function(){
            this.newTodoItem = '';
        }
    },
    components: {
        Modal: Modal
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
.closeModalBtn{
    color:#42b983;
  
}
</style>