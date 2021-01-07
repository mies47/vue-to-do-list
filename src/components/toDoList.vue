<template>
    <div class="toDoList-container">
        <h3 class="title bottomLine"> Tasks </h3>
        <select name="colorPicker" class="prioritySelect" v-model="filterBy">
            <option disabled value="">FilterBy Color</option>
            <option>All</option>
            <option>red</option>
            <option>yellow</option>
            <option>green</option>
        </select>
        <ul class="toDoList margin-top--medium">
            <list-item 
            v-for="item in dataLists.pinned" 
            :data="item" 
            :key="item.id"
            v-show="item.isShown" 
            v-on="$listeners"
            ></list-item>
            <list-item 
            v-for="item in dataLists.sortList" 
            :data="item" 
            :key="item.id" 
            v-show="item.isShown"
            v-on="$listeners"
            ></list-item>
            <list-item 
            v-for="item in dataLists.completed" 
            :data="item" 
            :key="item.id" 
            v-show="item.isShown"
            v-on="$listeners"
            ></list-item>
        </ul>

    </div>
</template>

<script>
import listItem from './listItem'
export default {
    props:{
        dataLists:{
            type:Object,
            required:true
        }
    },
    data() {
        return {
            filterBy: '',
        }
    },
    components:{
        listItem
    },
    methods: {
        filterItems:function(newValue , filterColor){
            if(filterColor === "") return;
            if(filterColor === "All"){
                Object.keys(newValue).forEach(function(key){
                    newValue[key].forEach(function(item){
                        item.isShown = true;
                    });
                });
                return;
            }
            Object.keys(newValue).forEach(function(key){
                newValue[key].forEach(function(item){
                    if(item.color !== filterColor) item.isShown = false;
                    else item.isShown = true;
                });
            });
        },
        
    },
    watch:{
        filterBy: function(newVal){
            this.filterItems(this.dataLists , newVal);
        }
    }
}
</script>

<style>
.toDoList-container{
    display: flex;
    width: 60%;
    margin: auto;
    justify-content: center;
    list-style: none;
    flex-direction: column;
    padding: 0;
}

.toDoList{
    display: flex;
    width: 100%;
    margin: auto;
    justify-content: center;
    list-style: none;
    flex-direction: column;
    padding: 0;
}
.title{
    text-align: left !important;
    padding-bottom: 5px;
}

.bottomLine{
    border-bottom: 1px solid #AAA;
}
</style>