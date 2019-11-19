<template>
  <div class="home">
    <!-- 이벤트 리스너 등록 -->
    <TodoForm @todoCreate-event="todoCreate"/> <!-- PascalCase, uppercamelcase -->
    <!-- kebab-case -->
    <TodoList :todos="todos"/>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios'
import TodoList from '@/components/TodoList.vue'
import TodoForm from '@/components/TodoForm.vue'

export default {
  name: 'home',
  components: {
    TodoList,
    TodoForm
  },
  data() {
    // 컴포넌트에서는 반드시 data를 함수로 작성하고, object로 리턴한다.
    return {
      todos: [],
    }
  },
  methods : {
    todoCreate(title) {
      console.log('==부모컴포넌트==')
      console.log('title')
    },
    getTodos() {
      axios.get('http://127.0.0.1:8000/api/v1/todos/')
      .then(response => {
        console.log(response) // 만약, 오류가 발생하게 되면 ESLint 설정을 package.json
        this.todos = response.data

      })
      .catch(error => {
        console.log(error)
      })
    }
  },
  mounted() {
    this.getTodos()
  }
}
</script>
