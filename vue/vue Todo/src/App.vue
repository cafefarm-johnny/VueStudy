<template>
  <div id="app">
    <!-- 등록한 지역 컴포넌트를 컴포넌트 태그를 만들어 연결한다. -->
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></TodoList> <!-- @는 v-on: 디렉티브의 약식 문법이다. -->
    <TodoFooter v-on:removeAll="clearAll()"></TodoFooter> <!-- TodoFooter.vue 컴포넌트로부터 removeAll 이벤트를 받는다. -->
  </div>
</template>

<script>
// ES6 문법으로 지역 컴포넌트를 등록하는 방법.
// import '불러온 파일의 내용이 담길 객체명' from '불러올 파일 위치'
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data() { // 해당 코드는 TodoList.vue 컴포넌트에서 하던 작업이 App.vue로 이동된 것이다.
    return {
      todoItems : []
    }
  },
  created() { // 해당 코드는 TodoList.vue 컴포넌트에서 하던 작업이 App.vue로 이동된 것이다.
    if (localStorage.length > 0)
    {
      for (let i = 0; i < localStorage.length; i += 1) 
      {
        this.todoItems.push(localStorage.key(i))
      }
    }
  },
  methods : {
    addTodo(todoItem) { // todoItem 값은 TodoInput.vue 컴포넌트로부터 전달받는다.
      localStorage.setItem(todoItem, todoItem)
      this.todoItems.push(todoItem)
    },
    clearAll() {
      localStorage.clear()
      this.todoItems = []
    },
    removeTodo(todoItem, index) {
      localStorage.removeItem(todoItem)
      this.todoItems.splice(index, 1)
    }
  },
  components : {
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
  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03)
  }
</style>
