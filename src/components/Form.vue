<template>

<div>
    <form @submit="handleSubmit">Skriv nytt inlägg<br><br>
        <input type="date" placeholder="YY/MM/DD" id="DateInput" style="width: 158px"><br><br>
        <textarea type="text" placeholder="Text" id="textInput" style="height: 80px"></textarea><br><br>
        <button>Save</button>
    </form>
    
</div>
    
</template>

<script>

export default {
    name: "dagbok",
    data(){
        return {
            Date: "",
            text: "",

        }
    },
    methods: {
        handleSubmit(event){
        
            
            console.log("Handle dagboksinlägg", event);

            this.$emit("save", event);
        }
    }
}

</script>

<style>

</style>
