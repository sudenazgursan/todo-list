<template>
  <div>
    <div class="form-element">
      <div class="item">
        <label>Todo Title</label>
        <input v-model="newTodoTitle" placeholder="New Todo Title">
      </div>
      <div class="item">
        <label>Todo Status</label>
        <select v-model="todoStatus">
          <option value="true">Completed</option>
          <option value="false">Not Completed</option>
        </select>
      </div>
      <button @click="addNewTodo">Add Todo</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  props: {
    todos: Array,
  },data() {
    return {
      newTodoTitle: '',
      todoStatus: null
    };
  },
  methods: {
    async addNewTodo() {
      try {
        const response = await axios.post('https://jsonplaceholder.typicode.com/todos', {
          title: this.newTodoTitle,
          completed: JSON.parse(this.todoStatus)
        });

        console.log(this.todoStatus);

        // Eklenen ToDo'yu listeye ekle
        this.todos.unshift(response.data);
      } catch (error) {
        console.error('Yeni ToDo eklenirken hata oluştu:', error);
      }
    }
  } 
};
</script>

<style scoped>
.form-element{
  display: flex;
  align-items: end;
  margin-bottom: 20px;
  gap: 10px;
}


.form-element .item{
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.form-element input,select{
  border:1px solid lightgray;
  padding: 8px 10px;
}

.form-element button{
  background:green;
  color:#fff;
  padding: 8px 10px;
  border-radius: 10px;
}
</style>
