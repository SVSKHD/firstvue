<template>
<div class="container">
<br class="mb-3"/>
<h1 class="text-center">Hello here is the New Tic Tac Toe</h1>
<hr/>
<main class="d-flex flex-column justify-content-center align-items-center">

<div class="row justify-content-center">
<div class="col col-6">
<div class="text-center">
<div v-if="!winMessage">
<h1 class="text-info" v-show="isCross">Cross Turn</h1>
</div>
<div v-if="!winMessage">
<h1 class="text-info" v-show="!isCross">Circle Turn</h1>
</div>
<div v-else>
<h1>{{winMessage.toUpperCase()}}</h1>
</div>
<div class="row">
<div 
v-for="(item , i) in itemArray"
:key="i"
@click="handleClick(i)"
class="card card-body col-md-4 mb-1 box justify-content-center align-items-center bg-light"
>
<Icon :iconname="item"/>
</div>
</div>
</div>
</div>
</div>

<hr/>
<button 
@click="reloadGame"
class="btn btn-danger">
Reset the Game
</button>


</main>
</div>
</template>

<script>
import Icon from './components/Icon.vue'
import Swal from 'sweetalert2/dist/sweetalert2.js'


export default {
name:"App",
components:{Icon},
data() {
return {
winMessage:"",
isCross:true,
itemArray:new Array(9).fill("empty")
}
},
watch:{
winMessage:function(message){
if(message){
this.showDialog()
}
}
},
methods:{

showDialog(){
Swal.fire({
icon:"info",
title:"Game Over",
text:`${this.winMessage}`
})
},

handleClick(itemNumber){
if(this.winMessage){
return this.showDialog()
}
if(this.itemArray[itemNumber]==="empty"){
this.itemArray[itemNumber] = this.isCross ? "cross" : "circle"
this.isCross = !this.isCross 
}else{
return Swal.fire("already Filled")
}
this.checkIsWinner()
},
 checkIsWinner() {
      //  checking  winner of the game
      if (
        this.itemArray[0] === this.itemArray[1] &&
        this.itemArray[0] === this.itemArray[2] &&
        this.itemArray[0] !== "empty"
      ) {
        this.winMessage = `${this.itemArray[0]} won`;
      } else if (
        this.itemArray[3] !== "empty" &&
        this.itemArray[3] === this.itemArray[4] &&
        this.itemArray[4] === this.itemArray[5]
      ) {
        this.winMessage = `${this.itemArray[3]} won`;
      } else if (
        this.itemArray[6] !== "empty" &&
        this.itemArray[6] === this.itemArray[7] &&
        this.itemArray[7] === this.itemArray[8]
      ) {
        this.winMessage = `${this.itemArray[6]} won`;
      } else if (
        this.itemArray[0] !== "empty" &&
        this.itemArray[0] === this.itemArray[3] &&
        this.itemArray[3] === this.itemArray[6]
      ) {
        this.winMessage = `${this.itemArray[0]} won`;
      } else if (
        this.itemArray[1] !== "empty" &&
        this.itemArray[1] === this.itemArray[4] &&
        this.itemArray[4] === this.itemArray[7]
      ) {
        this.winMessage = `${this.itemArray[1]} won`;
      } else if (
        this.itemArray[2] !== "empty" &&
        this.itemArray[2] === this.itemArray[5] &&
        this.itemArray[5] === this.itemArray[8]
      ) {
        this.winMessage = `${this.itemArray[2]} won`;
      } else if (
        this.itemArray[0] !== "empty" &&
        this.itemArray[0] === this.itemArray[4] &&
        this.itemArray[4] === this.itemArray[8]
      ) {
        this.winMessage = `${this.itemArray[0]} won`;
      } else if (
        this.itemArray[2] !== "empty" &&
        this.itemArray[2] === this.itemArray[4] &&
        this.itemArray[4] === this.itemArray[6]
      ) {
        this.winMessage = `${this.itemArray[2]} won`;
      }
    },
    reloadGame(){
      this.winMessage = "";
      this.isCross = true;
      this.itemArray = new Array(9).fill("empty")
    }

}

}
</script>

<style>
main {
  height: 100vh;
}
.grid {
  display: grid;
  grid-template-columns: 4fr 4fr 4fr;
  grid-gap: 5px;
}

.box {
  height: 150px;
}


</style>