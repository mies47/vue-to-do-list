<template>
    <div class="taskAdder">
        <h3 class="title bottomLine"> New Todo</h3>
        <input type="text" 
                v-model="inputText" 
                class="inputDescription"
                :class="{notValid: !validInput}"
                @keydown.enter.exact="submitTask"
                placeholder="Please enter what you want to do">
        <div class="selectContainer margin-top--medium">
            <select name="priority" class="prioritySelect" v-model.number="selectedPriority">
                <option disabled value="">Priority</option>
                <option value="3">High</option>
                <option value="2">Medium</option>
                <option value="1">Low</option>
            </select>
            <select name="colorPicker" class="prioritySelect" v-model="selectedColor">
                <option disabled value="">Color</option>
                <option>red</option>
                <option>yellow</option>
                <option>green</option>
            </select>
            <button class="submitBtn" @click="submitTask">submit</button>
        </div>
    </div>
</template>

<script>
export default {
    data:function(){
        return({
            inputText:'',
            selectedPriority:'',
            selectedColor:'',
            validInput:true
        })
    },
    methods:{
        submitTask: function(){
            if(this.inputText && this.selectedPriority && this.selectedColor){
                this.$emit('task' , {description: this.inputText , priority: this.selectedPriority , color: this.selectedColor, isShown:true});
                this.inputText = "";
                document.querySelector('.taskAdder .inputDescription').focus();
                this.validInput = true;
            }else{
                this.inputText = "Please enter task and select priority and color!";
                this.validInput = false;
                document.querySelector('.taskAdder .inputDescription').focus();
            }
        }
    }
}
</script>

<style>
.taskAdder{
    display: flex;
    flex-direction: column;
    justify-items: center;
    width: 60%;
    margin: auto;
    margin-top: 50px;
}

.inputDescription{
    text-align: center;
    height: 40px;
    border-radius: 20px;
    outline: none;
    border: 1px solid gray;
}

.inputDescription:focus , .prioritySelect:focus{
    border: 1px solid #7FDBFF;
}


.prioritySelect{
    background-color: white;
    /* reset */

    margin: 0;      
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    -webkit-appearance: none;
    -moz-appearance: none;
    /* background-color: white; */
    background-image:
    linear-gradient(45deg, transparent 50%, gray 50%),
    linear-gradient(135deg, gray 50%, transparent 50%),
    radial-gradient(#ddd 70%, transparent 72%);
    background-position:
        calc(100% - 20px) calc(1em + 2px),
        calc(100% - 15px) calc(1em + 2px),
        calc(100% - .5em) .5em;
    background-size:
        5px 5px,
        5px 5px,
        1.5em 1.5em;
    background-repeat: no-repeat;
    border: 1px solid #AAA;
    border-radius: 5px;
    padding: 8px;
    min-width: 100px;
}

.margin-top--medium{
    margin-top: 30px !important;
}

.submitBtn{
    border: none;
    border-radius: 20px;
    background-color:  #001f3f ;
    color: white;
    padding: 10px 15px;
    outline: none;
}

.title{
    text-align: left !important;
    padding-bottom: 5px;
}

.bottomLine{
    border-bottom: 1px solid #AAA;
}

.notValid{
    border: 1px solid red !important;
}
</style>