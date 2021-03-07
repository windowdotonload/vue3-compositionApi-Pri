<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Hello Vue 3.0 + Vite" />
  <h1>{{ count }}</h1>
  <h1>{{ refObj.a }}</h1>
  <h1>{{ read.name }}</h1>
  <button @click="add">click</button>
  <li v-for="(item, i) in state.arr" :key="i">{{ item }}</li>
  <p>{{ msg }}</p>
  <h1>{{ myRefData }}</h1>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import { ref, reactive, customRef, readonly } from 'vue'

function createFun() {
  let state = reactive({
    arr: [1, 2, 3]
  })

  return { state }
}

function myRef(v) {
  return customRef((track, trigger) => {
    return {
      get: function () {
        track()
        console.log('get', v)
        return v
      },
      set(nv) {
        console.log('set')
        v = nv
        trigger()
      }
    }
  })
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

    let refObj = ref({
      a: 'this is a in refObj'
    })

    let read = readonly({ name: 'this is readonly' })
    let { state } = createFun()
    let myRefData = myRef('this is myRefdata')

    function add() {
      count.value++
      // read = readonly({ name: 'afterchange readonly' })
      read = reactive({ name: 'after change' })
      refObj.value.a = 'change refOvj.a'
      myRefData.value = 'after change'
      state.arr.push(count.value)
    }

    return { count, add, state, myRefData, refObj, read }
  },
  data() {
    return {
      msg: 'this is data in options Api '
    }
  }
}
</script>
