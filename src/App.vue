<template>
  <div>
     <h3 class="text-info text-center p-3 bg-secondary">
        {{developer}}'s Todo App.
     </h3>
     <div class="container">
      <div class="row">
        <div class="d-flex justify-content-around align-items-center mt-3">
          <div>

            <input type="text" @keyup.enter="newTask()" class="me-1 " placeholder="task name" v-model="taskName" name="" id="">
            
            <button class="btn btn-info btn-sm" @click="newTask()">Create</button>
            <p class="text-danger" v-show="inputValidate">{{taskValidationText}}</p>
          </div>
          <div><span @click="ItemFilter" class="me-1 ">Hide Completed Task</span>
            <input type="checkbox" name="" id="" v-model="hide"></div>
        </div> 
    </div> <hr>
    <div class=" my-3 d-flex justify-content-between align-items-center">
      <span>Total : {{this.tasks.length}}</span>
      <button class="btn btn-sm btn-danger" @click="clear()">Tasks clear</button>
    </div>
    
      <div class="row ">
        <div class="col-6">
          <h5 class="text-center text-secondary">Tasks</h5>
        </div>
        <div class="col-6">
          <h5>
            <div class="text-center text-info">Status</div>
          </h5>
        </div>
      </div> 

      <div class="row" v-show="this.tasks.length == 0 ? 'dataCheck' : !'dataCheck'">
        <div class="col-12 mt-3"><h6 class="text-danger text-center">No data to show here. ...</h6></div>
      </div>
      
      <div class="row p-3" v-for="(item,index) in completedItemFilter" :key="index">
        <div class="col-6">
          <h6 class="text-center text-secondary " :class="item.state ? 'finishedSign': ''" >{{item.name}}</h6>
        </div>
        <div class="col-6">
          <h6>
            <div class="text-center text-info">
              <input type="checkbox" v-model="item.state">
            </div>
          </h6>
        </div>
      </div>
      
     </div>
  </div>
</template>

<script>
  export default{
    name : "App",

    data : ()=>({
      developer:'Pyae Phyo Thant',
      hide:false,
      taskName:'',
      taskValidationText:'where is your task name ?',
      inputValidate:false,
      dataCheck:true,
      tasks:[
        // { 'toMake':'Buy T-shirt','state':true },
      ],
    }),

    computed : {
        completedItemFilter(){
          return this.hide ? this.tasks.filter((v)=>v.state == false) : this.tasks;
        }
    },
    methods : {
      newTask(){
//validate text 
        this.dataCheck = false;
        this.inputValidate = this.taskName == '' ? true : false;
        if (this.inputValidate == false) {
          this.tasks.push({
          id:1,
          name: this.taskName,
          state:false,
        });
        this.taskName = '';
        }
      },
      clear(){
        this.tasks = [];

      }
    }
  };

</script>

<style>
  .finishedSign{
    text-decoration: line-through;
  }
</style>
