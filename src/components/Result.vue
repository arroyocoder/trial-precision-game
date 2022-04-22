<template>
   <div>
    <h1>Reaction Time is: {{ score }}</h1>
    <h1>{{ rank }}</h1>
  </div>
</template>

<script>
export default {
props: ['score'],
data(){
    return{
        rank: null
    }
},
mounted(){
    if(this.score < 250){
        this.rank = 'Very Fast'
    } else if(this.score < 400){
        this.rank = "No bad"
    } else{
        this.rank = "Too slow"
    }
}
}
</script>

<style>

</style>