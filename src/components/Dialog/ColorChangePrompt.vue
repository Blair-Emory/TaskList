<template>
  <q-dialog v-model="colorprompt" persistent>
    <q-card style="min-width: 350px">
      <q-card-section>
        <div class="text-h6">New Color</div>
      </q-card-section>

      <q-card-section>
        <q-color v-model="hex" no-header class="my-picker" />
      </q-card-section>

      <q-card-actions align="right" class="text-primary">
        <q-btn flat label="Cancel" v-close-popup />
        <q-btn flat label="Confirm" v-close-popup @click="colorprompt = false; addTask(); data = '';"/>
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<script>
export default {
  name: 'color-dialog',
  props:{
    hex:{
      type:String,
      required:true
    }
  },
  data(){
    return {
      hex:
    }
  }
}
</script>
