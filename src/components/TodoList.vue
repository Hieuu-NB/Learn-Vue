.
<template>
    <div id="app">
        <h1 style="color: red;">Todos List</h1>
        <!-- input -->
        <div>
            <input v-model="task" style="width:1200px;height:50px;text-indent:20px" type="text" placeholder="Enter Task">
            <button style="height: 50px;" @click="add()">SubmitTask</button>
        </div>
    
        <!-- task table -->
        <div id="tab">
            <div class="tab-content" @click="current=1">tat ca({{tasks.length}})</div>        
            <div class="tab-content" @click="current=2">da lam({{taskDone}})</div>        
            <div class="tab-content" @click="current=3">chua lam({{tasks.length - taskDone}})</div>        
        </div>

        <div v-show="current === 1" v-for="(task,index) in tasks" :key="index">
            <div class="list">    
                <button @click="task.isDone = !task.isDone;up(index)">Done</button>
                <div :class="{'gach-chan': task.isDone === true}">{{firstCharUpper(task.content)}}</div>
                <button @click="edit(index)">edit</button>
                <button @click="remove(index)">X</button>
            </div>  
        </div>

        <div v-show="current === 2"  v-for="(task,index) in tasks" :key="index+100">
            <div class="listt" v-if="task.isDone">
                <span>{{index+1}}.</span>
                <div>{{firstCharUpper(task.content)}}</div> 
            </div>
        </div>

        <div v-show="current === 3"  v-for="(task,index) in tasks" :key="index+1000">
            <div class="listt" v-if="!task.isDone">
                <span>{{index+1}}.</span>
                <div>{{firstCharUpper(task.content)}}</div>
            </div>
        </div>
    </div>    
</template> 

<script>

export default {
  data(){
    return{
        done:false,
        taskDone:0,
        editedTask:null,
        task:'',
        current:1,
        tasks:[
            {content:'di cho 1',isDone:false},
            {content:'di cho 2',isDone:false},
            {content:'di cho 3',isDone:false},
            {content:'di cho 4',isDone:false},
        ]
    }
  },
  methods:{
        add(){
            if(this.task.length === 0) return   
            if(this.editedTask === null) {
                this.tasks.push({content:this.task,isDone:false})
            }
            else{
                this.tasks[this.editedTask].content = this.task
                this.editedTask = null
            }
                this.task = ''
        },
        remove(index){
            this.tasks.splice(index,1)
            if(this.tasks.length < this.taskDone)
                this.taskDone--
            
        },
        firstCharUpper(str){
            return str.charAt(0).toUpperCase() + str.slice(1)
        },
        edit(index){
            this.editedTask = index
        },
        up(index){
            if(this.tasks[index].isDone === true)
                this.taskDone++
            else{
this.taskDone--
            }

        }
  
  }

  
}
</script>

<style scoped>
#app{
    margin-left: 100px;
    margin-top: 100px;
}
#tab{
    display: flex;
    justify-content: space-around;
    width: 1300px;
    border: 1px solid red;
    margin-top: 10px;
    height: 50px;
    line-height: 50px;
}
#tab div{
    cursor: pointer;
}
#tab div:hover{
    background: gray;
}
.list{
    display: flex;
    width: 1300px;
    justify-content: space-between;
    border:1px solid red;
    margin-top: 2px;
    height: 50px;
    line-height: 50px;
    color: red;
    font-size: 25px;
    background: yellow;
}

.listt{
    display: flex;
    justify-content: space-around;
    width: 1300px;
    margin-top: 2px;
    border:1px solid red;
    height: 50px;
    line-height: 50px;
}
.tab-content{
    cursor: pointer;
}
.gach-chan{
    text-decoration: line-through;
    color: gray;
}
.done{
    background: red;
}
</style>
