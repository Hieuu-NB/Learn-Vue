<template>
    <div>
        <!-- input --> 
        <div>
            <button @click="hide = !hide">+</button>
            <div v-show="hide==false">
                <input v-model="arr" type="text">
                <button @click="addTask(arr)">Ok</button>
            </div>
        </div>

        <!-- tab -->
        <div class="tab">

            <div>
                <div @click="pushTask(index)" v-for="(x,index) in Tasks1" :key="index">
                    {{x}}
                </div>
            </div>

            <div class="arrow">
                <button @click="swapBA()">↼</button>
                <button @click="swapAB()">⇁</button>
            </div>

            <div>
                <div @click="pushTask(index)" v-for="(y,index) in Tasks2" :key="index+100">
                    {{y}}
                </div>
            </div>
            
        </div>
    </div>
</template>

<script>
export default{
    data(){
        return{
            hide:true,
            arr:'',
            Tasks1:['1','2','2002' ],
            Tasks2:['3','4' ],
            Tasks3:[]
        }
    },
    methods:{
        addTask(arr){
            if(arr.length === 0)  this.hide = !this.hide 
            else{
                this.Tasks1.push(arr)
                this.arr=''
                this.hide= !this.hide
            }
        },
        pushTask(index){
            this.Tasks3.push(this.Tasks1[index])
            console.log(this.Tasks3);
        },

        swapAB(){
                this.Tasks2.push(this.Tasks3)
                this.Tasks1.splice(this.local,1)
                this.local=0
            },
        swapBA(){
            this.Tasks1.push(this.tasks2[this.local])
            this.tasks2.splice(this.local,1)
            this.local=0
        }
    }

}
</script>

<style scoped>
.tab{
    display: flex;
    margin:200px
}
.tab > div {
    display: block;
    width: 350px;
    border: 1px solid red;
}
.arrow button{
    display: block;
    margin-left: 36px;
    margin-top: 4px;
}
</style>

