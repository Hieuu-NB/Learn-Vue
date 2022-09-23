<template>
  <div id="app">
    <h1 style="color: red">Shopping</h1>
    
    

    <div class="head">
        <h2 style="color: red;">Danh sách sản phẩm đang bán :</h2>
        <div style="line-height: 70px;color:red">
            <input @click="swap =! swap" type="checkbox">
            <span>Option</span> 
        </div>
    </div>
    <div class="container">
        <div class="Iphone" v-for="(product,index)  in products" :key="index">

            <div>{{product.name | chuHoa}}</div> 
            <div v-show="swap == true">{{product.price | dauCham('vnd')}}</div>
            <div v-show="swap == false">{{product.price | dauPhay('vnd')}}</div>
            <button @click="add(index)">Buy</button>
        </div>
    </div>

    <h2 style="color: red;margin-left:300px">Danh sách đã chọn mua :</h2>

    <div v-show="boughts.length != 0" class="container">
        <div class="Iphone" v-for="(bought,index) in boughts" :key="index">
            <div>{{bought.name | chuHoa}}</div> 
            <div v-show="swap == true">{{bought.price | dauCham('vnd')}}</div>
            <div v-show="swap == false">{{bought.price | dauPhay('vnd')}}</div>
            <button @click="xoa(index)">Delete</button>
        </div>
    </div>
    
    <h2 v-show="boughts.length != 0" style="color: red;margin-left:300px;">Thành tiền</h2>
    <div v-show="boughts.length != 0" style="padding: 10px" class="price">
      <div>Tổng giá trị :</div> 
      <div v-show="swap == true">{{ boughts.reduce((total,p) => { return total+p.price},0) |  dauCham('vnd')}}({{boughts.reduce((total,p) => { return total+p.price},0)/23000 | soSauDauPhay }})</div>
      <div v-show="swap == false">{{ boughts.reduce((total,p) => { return total+p.price},0) |  dauPhay('vnd')}}({{boughts.reduce((total,p) => { return total+p.price},0)/23000 | soSauDauPhay }})</div>
    </div>

  
    



  </div>

</template>

<script> 

export default {
    data() {
      return {
        name:'Hieu',
        swap:true,
        products: [
          {name:'iphone 5 ',price:1000000},
          {name:'iphone 6 ',price:2000000},
          {name:'iphone 7 ',price:3000000},
          {name:'iphone 8 ',price:4000000},
          {name:'iphone 10 ',price:6500000},
          {name:'iphone 11 ',price:9000000},
          {name:'iphone 11 pro max ',price:12500000},
          {name:'iphone 13 pro max ',price:32500000},
        ],
        boughts:[ 

        ]
      }        
    },
    methods:{
        add(index){
            this.boughts.push(this.products[index])
        },
        xoa(index){
            this.boughts.splice(index,1)
        }
    },
    filters:{
      dauCham(x, donvi){
        return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g,".") + '' + donvi
      },
      dauPhay(x, donvi){
        return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g,",") + '' + donvi
      },
      chuHoa(x){
        return x.charAt(0).toUpperCase() + x.slice(1)
      },
      soSauDauPhay(x){
        return x.toFixed(2) + 'USD'
      }
    },
    
}
</script>
        
<style>
#app{
    background-image: linear-gradient(270deg,#ebeaeb,#c4ff57 95%);
    font-size: 18px;
    padding-bottom: 50px;
    padding-left: 50px;
}

.container{
    border: 3px solid red;
    margin-left: 400px;
    width: 400px;
}
.Iphone{
    display: flex;
    margin: 10px;
    justify-content: space-between;
    border-bottom: 1px solid red;
} 
.price{
    display: flex;
    justify-content: space-between;
    border: 3px solid red;
    margin-left: 400px;
    width: 400px;

}
.head{
    display: flex;
    width:460px;
    justify-content: space-between;
    margin-left:300px
}
</style>
          
