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
export default{
  name:'App',
  data(){
    return{
      todoText: '',
      todoList: []
    }
  },
  methods:{
    addTodo(){
      if(!this.todoText.trim()) return
      this.todoList.push({
        id: Date.now(),
        content: this.todoText
      })
      this.todoText=''
    },
    delTodo(row){
      this.todoList=this.todoList.filter(item=>item.id !== row.id)
    }
  }
}
</script>
<!--页面的逻辑，数据-->