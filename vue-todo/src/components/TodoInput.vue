<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" @keyup.enter="addTodo"> 
    <!--2way binding, input에 입력된 값을 동적으로 vue 인스턴스 안에 mapping 해줌-->
    <span class="addContainer" @click="addTodo">
      <i class="fa-solid fa-plus addBtn"></i>
    </span>
  </div>
</template>

<script>
export default {
  data: function(){
    return {
      newTodoItem: ''
    }
  },
  methods: {
    addTodo: function() {
      if (this.newTodoItem !== '') {
        var obj = {completed: false, item: this.newTodoItem}
        localStorage.setItem(this.newTodoItem, JSON.stringify(obj));
        // stringify : 객체를 string으로 변환해서 value값으로 넣어줌
        this.clearInput();
      }

    },
    clearInput: function(){
      this.newTodoItem='';
    }
  },
}
</script>

<style scoped>
input:focus {
  outline: none;
}

.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}

.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}

.addContainer {
  float: right;
  display: block;
  width: 3rem;
  background: linear-gradient(to bottom right, blue, pink);
  border-radius: 0 5px 5px 0;
}

.addBtn {
  color: white;
  vertical-align: middle;
}
</style>