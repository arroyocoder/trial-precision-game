<template>
  <div class="block" v-if="showBlock" @click="stopTimer">Hi there!!</div>
</template>

<script>
export default {
props: ['delay'], //delay prop is binded to delay data property in the App component
data(){
  return{
    showBlock: false,
    timer: null,
    reactionTime: 0
  }
},
mounted(){ //this fires whenever the component is mounted. Given the delay on setTimeout it will be mounted after the random miliseconds
  console.log('component is mounted');
  //setTimeout is a javascript method. Syntax is "setTimeout(function(){ alert("Hello"); }, 3000)"
  setTimeout(() => {
    this.showBlock = true
    this.startTimer()
  }, this.delay)
}, 
//Updated will fire after the component is mounted. in out case when the component is mounted after the setTimeout is fired
methods: {
  startTimer(){
    this.timer = setInterval(() => {
      this.reactionTime += 10
    }, 10) // in this function the timer property start adding 10 to reactionTime property every 10 miliseconds
  },
  stopTimer(){
    clearInterval(this.timer) // 
    this.$emit('end', this.reactionTime)
    this.showBlock = false
  } //in this function intervals of 10 miliseconds stored in timer property clears and the result incresement of reactionTime is also added as a value 
},
updated(){
  console.log('component is updated');
  
}
}
</script>

<style scooped>
.block {
  width: 400px;
  border-radius: 20px;
  background: orangered;
  color: black;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}
</style>