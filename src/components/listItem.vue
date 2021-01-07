<template>
    <li class="listItem" :class="{pinned: isPinned && !isDone , finished: isDone}">
        <div class="listItem-content" :class="{lineThrough: isDone}">{{ this.data.description }}</div>
        <div class="colorPreview" :style="{ 'background-color' : data.color }"></div>
        <button class="doneBtn" @click="done" :disabled="isDone"><i class="fas fa-check-circle"></i></button>
        <button class="pin" @click="pin" :disabled="isDone"><i class="fas" :class="{ 'fa-link': !isPinned , 'fa-unlink' : isPinned }"></i></button>
    </li>
</template>

<script>
export default {
    name: 'listItem',
    props:{
        data:{
            type:Object,
            required:true
        }
    },

    data:function(){
        return{
            isDone:false,
            isPinned:false
        }
    },

    methods: {
        done: function(){
            this.$emit('done' , this.data.id , this.isPinned);
            this.isDone = true;
        },
        pin: function(){
            this.isPinned = !this.isPinned;
            this.$emit('pin' , this.data.id , this.isPinned);
        }
    },
}
</script>

<style>
.listItem{
    width: 95%;
    border-radius: 20px;
    border: 1px solid  #AAA;
    display: flex;
    padding: 5px 2.5%;
    align-items: center;
    margin: 5px 0;
}

.listItem-content{
    width: 90%;
    text-align: left;
}

.doneBtn , .pin{
    background-color: transparent;
    border: none;
    outline: none;
    font-size: 20px;
}


.lineThrough{
    text-decoration: line-through;
    color: gray;
}

.listItem.pinned{
    border: 1px solid red !important;
}

.listItem.finished{
    border: 1px solid green !important;
}
.colorPreview{
    height: 10px;
    width: 10px;
    padding: 5px;
}
</style>