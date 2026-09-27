<template>
  <div id="app" style="padding:30px;">
    <!-- 输入框 + 添加按钮 -->
    <el-input v-model="todoText" placeholder="输入待办事项" style="width:300px;margin-right:10px;"></el-input>
    <el-button type="primary" @click="addTodo">添加</el-button>


    <!--  待办表格 -->
    <el-table :data="todoList" border style="width:500px;margin-top:20px;">
      <el-table-column prop="content" label="待办内容"></el-table-column>
      <el-table-column label="操作">
        <template slot-scope="scope">
          <el-button type="danger" size="mini" @click="delTodo(scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>
<!--页面长啥样有什么交互-->

<script>
export default {
  name:'App',
  data(){
    return{
      todoText: '',
      todoList: []
    }
  },
  mounted() {
    this.getTodoList()
  },
  methods:{
    async getTodoList() {
      const res=await this.$axios.get('http://localhost:3000/todos')
      this.todoList=res.data
    },
    async addTodo(){
      if(!this.todoText) return
      await this.$axios.post('http://localhost:3000/todos', {
        content: this.todoText
      })
      this.todoText=''
      this.getTodoList()
    },
    async delTodo(row){
      await this.$axios.delete(`http://localhost:3000/todos/${row.id}`)
      this.getTodoList()
    }
  }
}
</script>
<!--页面的逻辑，数据-->