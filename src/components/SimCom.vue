<template>
  <div>
    <h1>components zone</h1>
    <h1>{{id}}</h1>
    <v-btn color="success" @click="callMain()">callmain</v-btn>
  </div>
</template>

<script>

import {EventBus} from '@/EventBus'

export default {
  props:['id'],
  methods:{
    callMain(){
      // this.$emit('callAlertParam',this.id)
      EventBus.$emit('callAlertz')
    }
  }

}

</script>

<style>

</style>