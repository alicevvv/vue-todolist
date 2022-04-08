<template>
  <div class="container">
        <div class="d-flex flex-column justify-content-center align-items-center">
            <div class="title mt-5">My Todolist</div>

        <!--輸入事件區域-->
        <div class="addArea w-100 pt-3 d-flex justify-content-center">
            <input class="w-100 px-2" type="text" v-model.trim="newTask" @keyup.enter="addTask">
            <!--防止空白事件-->
            <button class="btn" v-on:click="addTask">+</button>
        </div>

        <!-- filter -->
        <!-- <div class="d-flex justify-content-center pt-3">
            <span class="ml-1 mr-1 button-choose">All</span>
            <span class="ml-1 mr-1 button-choose">Undo</span>
            <span class="ml-1 mr-1 button-choose">Done</span>
        </div> -->

        <!--清單列表-->
        <div class="listArea w-100 flex-column justify-content-center mt-3">
            <ul class="d-flex justify-content-center p-0" style="list-style-type: none;" >
                <li class="d-flex flex-row justify-content-between align-items-center my-2" v-for="(list,index) in lists" :key="index">
                    <div class="d-flex flex-row align-items-center mx-3">
                        <input type="checkbox" class="me-3" :id="'input'+index">
                        <label :for="'input'+index">{{list.name}}</label>
                    </div>
                    <img class="delete-btn mx-3" :src="trashImg" type="button" @click="remove(index)">
                </li>
            </ul>
        </div>
        </div>
    </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data(){
    return{
      newTask: '',
      lists: [{ name: "買牛奶", done: false }, { name: "唸日文", done: false }, { name: "閱讀", done: false }],
      certain: 'Add!',
      // favicon:require('./assets/icon/favicon.ico'),
      trashImg:require('./assets/img/trash.svg'),
    }
  },
  methods:{
    addTask: function() {
                if (this.newTask) {
                    this.lists.push({ name: this.newTask, done: false }); //把清單都push上去
                    this.newTask = '';
                } else { alert('不可輸入空白'); }

            },
            remove: function(index) {
              // 從第 index+1 個刪掉 1 個資料
                this.lists.splice(index, 1);
            }
  }
}
</script>

<style>
#app{
    background-color:#f5f5f5;
    min-height: 100vh;
}
.title {
    font-size: 32px;
    text-align: center;
    color: #2b2b2b;
    font-weight: bold;
}

.container{
    max-width: 800px !important;
}

.addArea input {
    height: 40px;
    border: #cacaca 2px solid;
    box-shadow: none;
    border-top-left-radius: 8px;
    border-bottom-left-radius: 8px;
    padding: 4px;
}
.addArea input:focus-visible{
    outline: none;
}
.addArea button{
    border: #cacaca 2px solid;
    color:#ffffff;
    background-color:#cacaca;
    border-top-left-radius: 0px;
    border-bottom-left-radius: 0px;
    border-top-right-radius: 8px;
    border-bottom-right-radius: 8px;
}
.addArea button:hover{
    opacity: 0.9;
}

ul {
    width:100%;
    flex-wrap: wrap;
}

li {
    width: 100%;
    height: 60px;
    border: #fcdea7 2px solid;
    border-radius: 8px;
    background-color: #fffed7;
}

input[type="checkbox"] {
    border: #cacaca 1px solid;
}

.delete-btn:hover {
    opacity: 50%;
}


@media screen and (max-width:415px) {
    ul {
        flex-wrap: wrap;
    }
    li {
        width: 80vw;
    }
}

</style>
