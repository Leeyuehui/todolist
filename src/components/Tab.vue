<template>
    <div id="tab">
       <header class="bar bar-nav">
                <button class="button button-link button-nav pull-left">
                <span class="icon icon-left"></span>
                    返回
                </button>
                <button class="button button-link button-nav pull-right"
                    @click="showInput"
                    >
                    新建
                <span class="icon icon-right"></span>
                </button>
                <h1 class="title">todolist</h1>
             </header>
    </div>
</template>


<script>

export default {
    methods: {
        showInput () {
            this.$bus.emit('change_input_flag')
        }
    }
}
</script>

<style lang="stylus" scoped>
#tab
    position fixed
    top 0
    left 0
    right 0
    z-index 2
   

   
</style>