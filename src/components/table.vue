<template>
  <div class="container">
    <add-component :todos="todos" />
    <div class="responsive-table">
      <table>
        <thead>
          <tr>
            <td>ID</td>
            <td>Todo Name</td>
            <td>Status</td>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in todos" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.title }}</td>
            <td>
              <span v-if="item.completed" class="badge success">Completed</span>
              <span v-else class="badge error">Not Completed</span>
            </td>
          </tr>
        </tbody>
    </table>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import AddComponent from '@/components/add.vue';

export default {
  components: {
    AddComponent
  },
  data() {
    return {
      todos: [],
    };
  },
  mounted() {
    this.getTodos();
  },
  methods: {
    async getTodos() {
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/todos?_start=0&_limit=5  ');
        this.todos = response.data;
      } catch (error) {
        console.error('ToDo listesi alınırken hata oluştu:', error);
      }
    }
  },
};
</script>


<style scoped>
.responsive-table {
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-bottom: 20px;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}

.badge{
  border-radius: 8px;
  color: #fff;
  padding: 6px;
  display: block;
  width: 150px;
  text-align: center;
}

.badge.error{
  background: red;
}

.badge.success{
  background: green;
}
</style>