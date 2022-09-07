<template>
    <div class="full-container">
       <div class="main-container">
           <div class="main-title">
               <h1>TODOLIST</h1>
           </div>
           <div class="main-content">
               <input type="text" placeholder="what needs to be done?"/>
               <button>+</button>
           </div>

       </div>
    </div>
</template>

<script>

export default {
    name: 'to-do-list',
    components: {},
    data() {
        return {

        }
    },
    methods : {



    }
}
</script>

<style>
body {
    background-color: #5E9ABE;
}

.full-container {
    display: flex;
    justify-content: center;
}

.main-container {
    margin-top: 30px;
    display: flex;
    background-color: white;
    width: 80%;
    align-items: center;
    flex-direction: column;

}

.main-content {
    width: 70%;
    padding-bottom: 30px;
}

.main-content input {
    height: 30px;
    width: 80%;
    text-align: center;
    border-color: #5E9ABE;
    /*border: none;*/
    border-radius: 5px;
}

.main-content button {
    margin-left: 10px;
    height: 35px;
    width: 35px;
    background-color: #5E9ABE;
    color: white;
    border: none;
    border-radius: 5px;

}


</style>
