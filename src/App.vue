<template>
  <div style="background: lightpink; width: 600px; height: 360px; padding: 20px; box-shadow: 10px 8px; border: 2px solid black"> 
  <div style="text-shadow: 3px 2px white; font-family: calibri; font-size: 20px">
    <h1>VUE DAGBOK</h1>
  </div>
  <div style="display: flex; flex-direction: row">
  <div style="border: 1px solid black; width: 200px; padding: 10px; box-shadow: 10px 8px; background: white ">
  <Form   @save="handleSubmit"  />
  </div>
  <div style="margin-left: 30px; margin-right: 30px; border: 1px solid black; padding-left: 5px; padding-right: 20px; padding-top: 10px; box-shadow: 10px 8px; background: white"> Dagboksinlägg:
  <ul v-for="post in this.dagboksArray" :key="post.date" style="margin-top: 10px"> 
    <li @click="getContent(post)" style="width: fit-content">{{post.date}}</li>
  
  </ul>
  </div>

  <div v-if='this.chosenDate !== ""' style="border: 1px solid black; height: 210px; width: 120px; max-width: 120px ; padding: 10px;box-shadow: 10px 8px; background: white">
   <b>{{chosenDate}}</b><br><br>
    {{chosenPost}} 

  

  </div>
  </div>
  </div>
  
</template>

<script>
import Form from './components/Form.vue'

export default {
  name: 'App',

  created(){
       
       if(localStorage.getItem("Posts") === null){
         console.log("local storage är tom")
         this.dagboksArray = []
       } else {
         console.log("inlägg finns i localStorage")
         this.dagboksArray = JSON.parse(localStorage.getItem("Posts")),
        
        this.dagboksArray.sort((a, b) => {
        let fa = a.date,
        fb = b.date

        if (fa < fb) {
        return -1;
         }
        if (fa > fb) {
        return 1;
        }
         return 0;
        });
         console.log(this.dagboksArray)
       }


     },
  
  updated(){
    console.log("something was updated please rerender", this.dagboksArray)
    //catch updates made to dagboksarray för att skippa fulrendering genom reload()

  },

  data(){
    return{
      
      dagboksArray: [],
      chosenPost: "",
      chosenDate: "",
      
      
      
     

    }
  },
  
  
  components: {Form},
  
  methods: {
    handleSubmit(event) {
      event.preventDefault();
      
     // console.log("formulär sparat!", event.target.DateInput.value + " " + event.target.textInput.value );
      this.dagboksArray.push({date:event.target.DateInput.value, text:event.target.textInput.value}),
      console.log(JSON.stringify(this.dagboksArray))
      localStorage.setItem("Posts", JSON.stringify(this.dagboksArray))
      //horrible solution to force the whole page to reload. will try to solve in another way, probably with life cycle hooks
      location.reload();
      
     
     },
     getContent(post){
       console.log(this.dagboksArray)
       console.log("clicked at", post.text)
       this.chosenPost = post.text
       this.chosenDate = post.date 
       

     },
     
    

  }
}

</script>

<style>

</style>
