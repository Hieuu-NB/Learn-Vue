         <template>
          <div id="app">
            <div class="header">
              <h3>Bảng công việc</h3>
              <button @click="add = !add">+</button>
            </div>

            <div v-show="add==false">
              <button @click="add = !add">X</button>
              <input type="text" v-model="content">
              <button @click="addTask()">OK</button>
            </div>



            <div class="lists">
              <div @click="currnetTab = '1'">Chưa làm</div>
              <div @click="currnetTab = '2'">Đã làm</div>
              <div @click="currnetTab = '3'">Tất cả</div>
            </div>
        
            <div v-show="currnetTab == '1'" class="tab" v-for="(task,index) in willDo" :key='index'>
              <input @click="task.isDone = !task.isDone" type="checkbox">
              <div :class="{ none: !task.isDone }" >{{task.name}}</div>
              <button @click="deleteTask(index)">X</button>
            </div>
        
            <div v-show="currnetTab == '2'" v-for="(task,index) in willDo" :key='index+1033'>
              <div class="tab"  v-if="!task.isDone">
                <input type="checkbox">
                <div>{{task.name}}</div>
                <button>X</button>
              </div>
            </div>
        
            <div v-show="currnetTab == '3'" v-for="(task,index) in willDo" :key='index+100'>
              <div class="tab" >
                <div :class="{ none: !task.isDone }">{{task.name}}</div>
                <button @click="deleteTask(index)">X</button>
              </div>
            </div>
          </div>
        </template>
        <script>
        export default {
            data() {
                return {
                  content:'',
                  add:true,
                  active: false,
                  currnetTab: '1',
                  willDo:[
                    {
                      name:"di cho",
                      isDone:true
                    },
                    {
                      name:"nau com",
                      isDone:true
                    },
                    {
                      name:"giat do",
                      isDone:true
                    },
                  ]
                };
            },
            methods:{
              deleteTask(index){
                this.willDo.splice(index,1)
                // this.willDo.remove(willDo[index])
              },
              addTask(){
                this.add = !this.add
                this.willDo.push({name:this.content,isDone:true})
                this.content = ''
              }
            }
        }
        </script>
        
        <style scoped>
        #app{
          border: 1px solid red;
          display: inline-block;
          width: 400px;
          border-radius: 5px;
          overflow: hidden;
        }
        .header{
          display: flex;
          justify-content: space-between;
          padding-left: 20px;
          padding-right: 20px;
          border-bottom: 1px solid red;
          background: linear-gradient(to bottom right, red, yellow);
          color: white;
        }
        .header>button{
          display: block;
          width: 25px;
          height: 25px;
          margin-top: 17px;
        }
        .lists>div{
          display: inline-block;
          width: 23%;
          padding-left: 40px;
          height: 40px;
          line-height: 40px;
          border: 0.66px solid red;
        }
        .lists > div:focus {
          background-color: red;
        }
        .lists > div:hover {
          background-color: yellowgreen;
        }
        .tab{
          display: flex;
          padding: 5px;
        }
        .tab > input{
          display: block;
          width: 20px;
          height: 20px;
          background: red;;
        }
        .tab > div{
          display: block;
          width: 335px;
          padding-left: 10px;
        }
        .tab >  button{
        
        }
        .none{
          text-decoration: line-through;
        }
        </style>
          
