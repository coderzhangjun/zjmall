<template>
<div class="tab-control">
<div class="tab-control-item"
        v-for="(item,index) in titles " 
        :class="{active: currentIndex===index}"
        
        @click="itemClick(index)">
    <span>{{item}}</span>
   </div>
</div>
   
</template>

<script>
export default {
name:"TabControl",
props:{
    titles:{
        type:Array,
        default(){
            return []
        }
    }
},
data(){
   return{
       currentIndex:0
   } 
},
methods:{
    itemClick: function(index){
          this.currentIndex =  index
           this.$emit('tabclick', index);
    }
}
}
</script>

<style scoped>
.tab-control {
display: flex;
background-color: #fff;
position: sticky;
top: 44px;
z-index: 10;
}

.tab-control-item {
    text-align: center;
    flex: 1;
}

.active {
    color: var(--color-high-text);;
}
.active span {
    border-bottom: 2px solid var(--color-high-text);
}
</style>