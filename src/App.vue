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
      <div>
        <button class="btn btn-sm btn-danger me-1" @click="clear()">All clear</button>
      <button class="btn btn-sm btn-danger" @click="ctc()">Completed Tasks clear</button>
      </div>
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
          
          <h6 class="text-center text-secondary " :class="item.state ? 'finishedSign': ''" > {{  item.name}}</h6>
        </div>
        <div class="col-6">
          <h6>
            <div class="text-center text-info">
              <input type="checkbox" v-model="item.state" @click="checkboxcheck(index)">
              
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
          name: this.taskName,
          state:false,
        });
        localStorage.setItem("localTasks",JSON.stringify(this.tasks));
        this.taskName = '';
        }
      },
      clear(){
        this.tasks = [];
        localStorage.setItem("localTasks",JSON.stringify(this.tasks));

      },
      ctc(){
        // alert('you clicked completed task clear button');
        this.tasks = this.tasks.filter((x)=> x.state !== true);
        localStorage.setItem("localTasks",JSON.stringify(this.tasks));

      },
     
    },
    // beforeCreate() {
    //   console.log('before create'); 
    // },
    // mounted() {
    //    console.log('mounted');
    // },
    // beforeMount(){
    //   console.log('before mount');
    // },
    // created() {
    //    console.log('created');
    // },

  // Local Storeage tests  --> we can use except BeforeCreate(); others OK!!!!!!
  beforeMount() {
    let lcData = localStorage.getItem("localTasks");
    if (lcData !== null) {
      this.tasks = JSON.parse(lcData);
      console.log(this.tasks);
    }
  },
  };

</script>

<style>
  .finishedSign{
    text-decoration: line-through;
  }
</style>
