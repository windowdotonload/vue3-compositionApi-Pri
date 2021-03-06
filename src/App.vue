<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Hello Vue 3.0 + Vite" />
  <h1>{{count}}</h1>
  <button @click='add'>click</button>
  <li v-for='(item,i) in state.arr' :key='i'>{{item}}</li>
  <p>{{msg}}</p>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import {ref,reactive} from 'vue'

function createFun(){
  let state = reactive({
    arr:[1,2,3]
  })

  return {state}
}

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  setup(props) {
    let count = ref(0)
    // let state = reactive({
    //   arr:[1,2,3]
    // })

    let {state} = createFun() 

    function add () {
      count.value++
      state.arr.push(count.value)
    }

    return {count,add,state}
  },
  data(){
      return {
        msg:"this is data in options Api "
      }
    }
}
</script>
