<template>

<div style="background: white; border: 1px Solid black; margin-left: 20px">
    <ul v-for="object in dagboksArray" :key="object.date" style="margin-top: 10px"> 
    <li @click="getContent(object)" style="width: fit-content">{{object.date}}</li>
  
  </ul>
    <div v-if='this.chosenDate !== ""' style="border: 1px solid black; height: 230px; width: 120px; max-width: 120px ; padding: 10px;box-shadow: 10px 8px; background: white; position:relative; left: 160px">
   <b>{{chosenDate}}</b><br><br>
    {{chosenPost}} 

  

  </div>
     
</div>
    
</template>

<script>

export default {
    name: "Build",
    data(){
        return {
            
            Date: "",
            text: "",

        }
    },
    props: ['dagboksArray','chosenDate'], 
    methods: {
        getContent(object){
       console.log(this.dagboksArray)
       console.log("clicked at", object.text)
       this.chosenPost = object.text
       this.chosenDate = object.date 
       

     }
        
    }
}

</script>

<style>

</style>
