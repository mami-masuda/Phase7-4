<template>
  <div>
    <h1>Todoリスト</h1>
    <form @submit.prevent="addTodo()">
      <el-input v-model="todo" type="text" placeholder="todo"></el-input>
    </form>
    <el-row gutter="10">
       <el-col :span="12" v-for="( todo, index ) in todos" :key="index">
          <el-card class="box-card">
            {{ todo }} 
            <el-button @click="removeTodo(index)" type="success" icon="el-icon-check" circle ></el-button>
          </el-card>
        </el-col>
    </el-row>
  </div>
</template>

<style>
  .el-row {
    margin-bottom: 40px;
    }
</style>


<script>
export default{
  name: 'TodoList',
  data(){
    return{
      todo: '',
      todos:[]
    }
  },
  methods: {
    addTodo(){
      this.todos.push(this.todo);
      this.todo = '';
    },
    removeTodo(index){
      this.todos.splice(index,1);
    },
  }
}
</script>


