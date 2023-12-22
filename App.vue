<template>
  <div>
    <h1 class="h1">::::: Vue Todo List :::::
      <span></span>
    </h1>
    <span>
    <div class="adding">
      <input class="type" v-model="newTask" @keyup.enter="addTask" placeholder="輸入待辦事項..."> 
      <button class="addButton" @click="addTask">新增！</button> 
    </div>
    </span>
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <input class="checkbox" type="checkbox" v-model="task.completed"> {{ task.text }} 
        <button class="delete" @click="removeTask(index)">刪除！</button> 
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',  
      tasks: []   
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {   
        this.tasks.push({ text: this.newTask, completed: false });
        this.newTask = ''; 
        this.saveToLocalStorage();
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1); 
      this.saveToLocalStorage(); 
    },
      saveToLocalStorage() {
        // 將 tasks 數據轉換為 JSON 字符串，並保存到本地存儲中的 "todo-list" 鍵
        localStorage.setItem('todo-list', JSON.stringify(this.tasks));
      },
      loadFromLocalStorage() {
        // 從本地存儲中讀取 "todo-list" 鍵的值，解析為對象，並賦值給 tasks
        const savedTasks = localStorage.getItem('todo-list');
        if (savedTasks) {
          this.tasks = JSON.parse(savedTasks);
        }
      }
    },
  mounted() {
    this.loadFromLocalStorage(); // 組件掛載後，載入本地存儲中的數據
  }
};
</script>

<style scoped>
  h1{
    text-align: center;
    text-shadow: 1px 1px 3px #618AEF, -2px -2px 6px #41B883;
    color: #618AEF,#41B883 ;
    background-color:#35495E;
    font-size: 40px;
    width: auto;
  }
  .type{
    height: 90px;
    width: 250px;
    font-size: xx-large;
    display:inline;
    margin-right: 50px;
  }

  .adding{
    margin-top: 50px;
    margin-bottom: 50px;
  }

  div{
    text-align: center;
  }

  .addButton,
  .addButton:hover,
  .addButton:focus {
      display: inline;
      font-size: x-large;
      font-weight: 900;
      text-shadow: 0px 0px 7px #c1dffe;

      align-items: center;
      justify-content: center;
      z-index: 1;
      width: 100px;
      height: 100px;
      border-radius: 50%;
      border: none;
      background: #41B883;
      color: #35495E;
      transition: box-shadow 400ms cubic-bezier(0.2, 0, 0.7, 1), transform 200ms cubic-bezier(0.2, 0, 0.7, 1);
  }
  .addButton:hover {
      transform: rotate(360deg);
      box-shadow: 0 0 1px 15px #33475c40 , 0 0 1px 30px #455F7B30 , 0 0 1px 45px #668DB610 ;
  }
  ul{
    font-size: xx-large;
    text-align: center;
  }
  li{
    padding-top: 15px;
    padding-bottom: 15px;
    border-bottom: 4px dotted #35495E;
  }
  .checkbox{
    width: 50px;
    height: 50px;
    vertical-align: middle;
  }
  .completed {
    text-decoration: line-through; /* 加上刪除線 */
  }

  .delete,
  .delete:focus {
    margin-left: 50px;
    margin-right: 10px;
    vertical-align: middle;
    background: transparent;
    color: #a44f4c;
    font-size: 1rem;
    text-align: center;
    text-transform: uppercase;
    text-decoration: none;
    box-sizing: inherit;
    padding: 15px 40px;
    border: 1px solid;
    box-shadow: inset 0 0 20px rgba(225, 51, 45, 0);
    outline: 1px solid !important;
    outline-color: rgba(225, 51, 45, 0.5);
    outline-offset: 0px;
    text-shadow: none;
    transition: all 1250ms cubic-bezier(0.19, 1, 0.22, 1);
  }
  .delete:hover {
    color: #924341;
    border: 1px solid;
    box-shadow: inset 0 0 20px rgba(225, 51, 45, 0.5), 0 0 20px rgba(225, 51, 45, 0.2);
    outline: 1px solid !important;
    outline-color: rgba(225, 51, 45, 0) !important;
    outline-offset: 15px;
    text-shadow: 1px 1px 2px rgba(255, 0, 0, 0.4);

  }

</style>
