<template>
  <div>
    <ul>
      <li v-for="(todoItem, i) in todoItems" :key="i" class="shadow">
        <i class="fa-solid fa-square-check checkBtn" :class="{checkBtnCompleted : todoItem.completed}" @click="toggleComplete(todoItem)"></i>
        <span :class="{textCompleted : todoItem.completed}">{{ todoItem.item }}</span>
        
        <span class="removeBtn" @click="removeTodo(todoItem, i)">
          <i class="fa-solid fa-delete-left"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      todoItems: []
    }
  },
  methods: {
    removeTodo: function(todoItem, i) {
      localStorage.removeItem(todoItem.item); //localStorage에서 삭제
      this.todoItems.splice(i, 1); //data의 todoItems배열에서 삭제
    },
    toggleComplete: function(todoItem) {
      if(todoItem.completed == false){
        todoItem.completed = true;
        localStorage.removeItem(todoItem.item);
        localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
      }else{
        todoItem.completed = false;
        localStorage.removeItem(todoItem.item);
        localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
      }
      
    }
  },
  // localStorage에 항목 있으면 todoItems에 추가함
  created: function() {
    if (localStorage.length > 0) {
      for(var i=0; i<localStorage.length; i++) {
        if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
          //todoItems에 객체를 넣어줌 (JSON.parse는 string을 다시 객체로 변환해줌)
        }
      }
    }
  },
}
</script>

<style scoped>
  ul {
    list-style-type: none;
    padding-left: 0;
  }
  li {
    display: flex;
    height: 50px;
    line-height: 50px;
    background: white;
    border-radius: 5px;
    padding: 0 0.9rem;
    margin: 0.5rem 0;
  }
  .removeBtn {
    margin-left: auto;
    color: black;
  }
  .checkBtn {
    color: gray;
    line-height: 50px;
    margin-right: 15px;
  }
  .checkBtnCompleted {
    color: blueviolet
  }
  .textCompleted {
    text-decoration: line-through;
    color: gray;
  }
</style>