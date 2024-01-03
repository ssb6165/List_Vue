<script setup>
import { shuffle as _shuffle} from 'lodash'
import { ref } from 'vue'

const getInitialItems = () => [1,2,3,4,5]
const items = ref(getInitialItems())
let id = items.value.length + 1

function insert(){
  const i = Math.round(Math.random() * items.value.length)
  items.value.splice(i, 0, id++)
}

function reset(){
  items.value = getInitialItems()
  id = items.value.length + 1
}

function shufffle(){
  items.value = _shuffle(items.value)
}

function remove(item){
  const i = items.value.indexOf(item)
  if(i>-1){
    items.value.splice(i,1)
  }
}
</script>

<template>
  <button @click="insert"> 랜덤 인덱스 삽입 </button> 
  <button @click="reset"> 초기화 </button>
  <button @click="shufffle"> 순서 바꾸기 </button>

  <TransitionGroup tag="ul" name="fade" class="container">
    <div v-for="item in items"  class="item" :key="item">{{ item }}
    <button @click="remove(item)">X</button>
    </div>
  </TransitionGroup>
</template>

<style>
.container{
  position: relative;
  padding: 0;
}

.item{
  width: 100%;
  height: 30px;
  background-color: #f3f3;
  border: 1px solid #666;
  box-sizing: border-box;
}

.fade-move,
.fade-enter-active,
.fade-leave-active{
  transition: all 0.5s cubic-bezier(0.55, 0, 0.1, 1);
}

.fade-enter-from,
.fade-leave-to{
  opacity: 0;
  transform: scaleY(0.01)
  translate(30px, 0);
}

.fade-leave-active{
  position: absolute;
}
</style>