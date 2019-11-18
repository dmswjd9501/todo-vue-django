<template>
  <div class="home">
    
    <TodoList/>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios'
import TodoList from '@/components/TodoList.vue'

export default {
  name: 'home',
  components: {
    TodoList
  },
  data() {
    // 컴포넌트에서는 반드시 data를 함수로 작성하고, object로 리턴한다.
    return {
      todos: [],
    }
  },
  mounted() {
    // axios 요청
    axios.get('http://127.0.0.1:8000/api/v1/todos')
      .then(response => {
        console.log(response) // 만약, 오류가 발생하게 되면 ESLint 설정을 package.json
      })
  }
}
</script>
