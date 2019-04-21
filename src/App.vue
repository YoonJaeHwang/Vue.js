<template> 
    <div id="app">
      <!-- 등록된 컴포넌트 4개를 HTML에 표시 -->
      <TodoHeader></TodoHeader> 
      <TodoInput v-on:addTodo="addTodo"></TodoInput>
      <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></TodoList>
      <TodoFooter v-on:removeAll="clearAll"></TodoFooter> 
    </div>
</template>

<script> 
import TodoHeader from './components/TodoHeader.vue' // 컴포넌트 내용을 불러오기 위한 ES6 import 구문
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default { // 지역 컴포넌트 등록
    created() {
        if (localStorage.length > 0) {
            for(var i = 0; i < localStorage.length; i++) {
                this.todoItems.push(localStorage.key(i));
            }
        }
    },
    data() {
        return {
            todoItems:[] // 데이터 속성 todoItems 선언 
        }
    },
    methods: {
    addTodo(todoItem) {
        localStorage.setItem(todoItem, todoItem);
        this.todoItems.push(todoItem);
        },
    clearAll() {
        localStorage.clear();
        this.todoItems = [];
        },
    removeTodo(todoItem, index) {
            localStorage.removeItem(todoItem);
            this.todoItems.splice(index, 1);    
        }        
    },
    components: {
      'TodoHeader' : TodoHeader,
      'TodoInput' : TodoInput,
      'TodoList' : TodoList,
      'TodoFooter' : TodoFooter
    }
}
</script>

<style>
  body {
        text-align: center;
        background-color: #F6F6F8;
    }

    input {
        border-style: groove;
        width: 200px;
    }

    button {
        border-style: groove;
    }

    .shadow{
        box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03)
    } 
</style>
