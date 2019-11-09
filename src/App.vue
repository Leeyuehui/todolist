<template>
  <div id="app">
    <tab></tab>
    <Container :todos = "newTodos"
               @change_flag = "changeFlag"
               @check = 'check'
               @add_item = 'addItem'
              >
    </Container>
    <myMask v-if="mask_flag"
            :close_mask="closeMask"
            :remove = "remove"
            :active_index = 'active_index'
          >
    </myMask>
    <Footer @get_type= "changeType"
            :type = "type"></Footer>

  </div>
</template>

<script>
import Tab from './components/Tab.vue'
import Container from './components/Container.vue'
import Footer from './components/Footer.vue'
import myMask from './components/myMask.vue'


export default {
  name: 'app',
  components: {
    Tab,Container,Footer,myMask
  },
  data () {
    return {
      mask_flag: false,
      active_index: 0,
      type: 'A',
      todos: [
        {
          id: 1,
          task: `任务1`,
          info: '任务一内容111',
          done:true
       },
        {
          id: 2,
          task: '任务2',
          done: true,
          info: '任务二内容'
        },
        {
          id: 3,
          task: '任务3',
          info: '任务三内容',
          done: true
        }
      ]
    }
  },
  methods:{
    changeFlag ( index ) {
      this.todos[index].done = ! this.todos[index].done
    },
    check ( index ) {
      const flag = this.todos[index].done
      if ( flag ) {
        this.remove()
      } else {
       this.active_index = index
       this.changMaskFlag()
      }
    },
    remove ( index ) {
       this.todos.splice( index , 1)
    },
    changMaskFlag () {
      this.mask_flag = true
    },
    closeMask () {
      this.mask_flag = false
    },
    addItem ( val ) {
      this.todos.push({
        id: sort(this.todos)[0].id + 1,
        task:`任务`,
        info: val,
        done: true, 
      })
    },
    changeType ( val ) {
            this.type = val
        }
  
  },
    computed: {
         newTodos () {
             switch ( this.type ) {
                 case 'A':
                     return this.todos
                     break;
                 case 'F':
                     return this.todos.filter( item => item.done)
                     break;
                 case 'U':
                     return this.todos.filter( item => !item.done)
                     break;
             }
         }
     }
  
}

function sort( arr ) {
    return arr.sort( function ( a, b){
        return b.id-a.id
    })
  }
</script>

<style lang="stylus" scoped>

</style>
