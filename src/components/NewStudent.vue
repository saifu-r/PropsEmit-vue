<template>
  <div>
     <form @submit.prevent="submitData"> <!--prevent so that the page doesn't reload -->
      <div>
        <label>ID</label>
        <input type="text" v-model="enteredId"/>
      </div>
      <div>
        <label>Name</label>
        <input type="text" v-model="enteredName"/>
      </div>
      <div>
        <label>Email</label>
        <input type="email" v-model="enteredEmail"/>
      </div>
      <div>
        <button>Add Contact</button>
      </div>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  emit: ["add-contact"],
  setup(props, {emit}) {
    const enteredId = ref('');
    const enteredName = ref('');
    const enteredEmail = ref('');

    const submitData= ()=>{
        emit('add-contact', enteredId.value, enteredName.value, enteredEmail.value)
    }

    return {enteredId, enteredName, enteredEmail, submitData}
  },
});
</script>

<style scoped>
</style>
