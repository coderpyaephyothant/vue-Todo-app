<template>
  <div>
     <h3 class="text-info text-center p-3 bg-secondary">
        {{developer}}'s Todo App.
     </h3>
     <div class="container">
      <div class="row pt-3">
        <div class="col-6">
          <h5 class="text-center text-secondary">Tasks</h5>
        </div>
        <div class="col-6">
          <h5>
            <div class="text-center text-info">Status</div>
          </h5>
        </div>
      </div> <hr>
      <div class="row p-3" v-for="(item,index) in tasks" :key="index">
        <div class="col-6">
          <h6 class="text-center text-secondary">{{item.toMake}}</h6>
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
      tasks:[
        { 'toMake':'Buy T-shirt','state':true },
        { 'toMake':'Buy Flanel-shirt','state':true },
        { 'toMake':'Buy Waterproof','state':false },
        { 'toMake':'Buy Facewash','state':true },
      ],
    }),
  };

</script>

<!-- <style>

</style> -->
