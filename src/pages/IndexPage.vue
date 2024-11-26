<template v-cloak>
  <q-page v-touch-pan.prevent.mouse="handlePan" class="flex flex-center text-white">
    <div class="row">
      <q-input
      v-model="data.name"
       placeholder="Counter"
      input-class="text-center text-h5 text-white"
      color="white"
      filled />
    </div>

 <div class="row full-width items-center">
 <div class="col text-center">
  <q-btn
  @click="decreaseCounter"
  v-touch-repeat:300:300:300:300:50.mouse="decreaseCounter"
   icon="remove"
  size="xl"
  round />
 </div>
 <div class="col text-center text-h2">
  {{ data.counter }}
 </div>

 <div class="col text-center">
  <q-btn
  @click="increaseCounter"
   v-touch-repeat:300:300:300:300:50.mouse.enter.space="increaseCounter"

  icon="add"
  size="xl"
  round />
 </div>

</div>
<div class="row">
  <q-btn @click="refresh" icon="refresh"
  size="xl"
  round />
 </div>
  </q-page>
</template>
<style scoped>
.q-page{
  max-width:700px;
  margin: 0 auto;
}
</style>

<script setup>
/*imports*/
import {reactive, watch} from 'vue'
import { useQuasar } from 'quasar'
/*data*/
 const data = reactive({
  counter:0,
  name:''

 })
 const $q = useQuasar()
 const savedData=$q.localStorage.getItem('data')
 if (savedData) Object.assign(data,savedData)
 watch(data, value =>{
  $q.localStorage.set('data', value)
 })
/* const savedData = $q.localStorage.getItem('data')
 if(savedData) Object.assign(data,savedData)
 watch(data, value =>{
    console.log(value)
    $q.localStorage.set('data', value)
 })*/


 /**Counter methods */
const increaseCounter = () => {

  data.counter++

}
const decreaseCounter = () => {
  if(data.counter>0){
  data.counter--}
}
const refresh = ()=>
{
  data.counter=0;
}
/**touch pan */
const handlePan = e => {
  if(e.delta.y < 0) increaseCounter()
  else decreaseCounter()
}
</script>
