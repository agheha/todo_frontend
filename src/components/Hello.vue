<template>
  <div class="hello">
    오늘 해야 할 일
    <ul v-if="toDoItems && toDoItems.length">
      <li v-for="toDoItem of toDoItems" v-bind:key="toDoItem">
        {{ toDoItem.title }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'hello',
  data: () => {
    return {
      toDoItems: [] // 빈 리스트로 초기화
    }
  },
  created() {
    // 초기화 함수
    axios
      .get('http://127.0.0.1:5000/todo/') // http://localhost:5000/todo/에 get call
      .then(response => {
        this.toDoItems = response.data.map(r => r.data) // 반환되는 값을 toDoItems에 저장
      })
      .catch(e => {
        console.log('error : ', e)
      })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #35495e;
}
</style>
