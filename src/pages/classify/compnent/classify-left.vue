<template>
    <div>
         <div class="calssify-left" ref="wrapper">
            <ul class="calssify-left-ul" >
                <li v-for="(list,index) in left" :key="index" @click="qiehuan(index)" :class="{active:index===classifyIndex}">
                    {{list.name}}
                </li>
            </ul>
        </div>
    </div>
</template>


<style lang="stylus" scoped>

        
</style>



<script>
export default {
    
}
</script>
