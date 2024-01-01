<template>
  <div>
    <div class="name">
      <h2>{{ propsName }} {{ isFavorite ? '- ♡': '' }}</h2>
      
      <button @click="toggleDetails">{{ showDetails ? 'Hide' : 'Show' }}</button>
      <button @click="toggleFavorite">{{ isFavorite ? 'Dislike' : 'Like' }}</button>
      <button @click="deleteContact">Delete</button>
      <ul v-if="showDetails">
        <li>{{ propsEmail }}</li>
      </ul>

    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  props: {
      id: {
        type: String,
        required: true
      },
      name: {
        type: String,
        required: true
      },
      email: {
        type: String,
        required: true
      },
      isFavorite: {
        type: Boolean,
        required: false,
        default: false
      },
      
    },
  emits: ['toggle-favorite', 'delete'],


  // emits:{
  //   'toggle-favorite': function(id: string){
  //     if(id){
  //       return true
  //     }else{
  //       return false
  //       // console.warn('id is missing')
  //     }
  //   }
  // },
  // these lines of code optional 
  // they are useful when developing something with team, so that everyone understands
  setup(props, {emit}) {

    const propsId= ref(props.id)
    const propsName= ref(props.name)
    const propsEmail= ref(props.email)
    // const propsIsFavorite= ref(props.isFavorite)

    const showDetails= ref(false)
    const toggleDetails= ()=>{
      showDetails.value= !showDetails.value
    }

    const toggleFavorite= ()=>{
      emit('toggle-favorite', propsId.value)
    }

    const deleteContact= ()=>{
      emit('delete', propsId.value)
    }

    return {propsId, propsName, propsEmail, showDetails, toggleDetails, toggleFavorite, deleteContact}

    
  },
});
</script>

<style scoped>


</style>
