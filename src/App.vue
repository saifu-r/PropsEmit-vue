<template>
  <div>
    <new-student
    @add-contact="addContact"
    />
    <FindContact 
    v-for="friend in friends"
    :key="friend.id"
    :id="friend.id"
    :name="friend.name"
    :email="friend.email"
    @toggle-favorite="favoriteStatus"
    :isFavorite="friend.isFavorite"
    @delete="deleteContact"/>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import FindContact from "./components/FindContact.vue";
import NewStudent from "./components/NewStudent.vue";

export default defineComponent({
  name: "App",
  components: { FindContact, NewStudent },
  setup() {
    const friends= ref([
      {
        id: "121",
        name: "Saifur Rahman",
        email: "saifur@gmail.com",

      },
      {
        id: "131",
        name: "Rakib Hossain",
        email: "rakib@gmail.com",
        isFavorite: false
      },
    ]);

    const favoriteStatus= (friendId: string)=>{
      // alert("hello from the other side")
      const identifiedFriend=  friends.value.find(friend => friend.id === friendId)

      // alert(friendId)

      if(identifiedFriend){
        identifiedFriend.isFavorite = !identifiedFriend.isFavorite
        // alert(identifiedFriend.isFavorite)
      }

      // identifiedFriend?.isFavorite = !identifiedFriend?.isFavorite
    }

    const addContact= (id: string, name: string, email: string)=>{
      const newStudent= {
        id: id,
        name: name, 
        email: email

      }
      friends.value.push(newStudent)
    }

    const deleteContact= (friendId: string)=>{
      friends.value= friends.value.filter((friend) => friend.id !== friendId)

      // alert(friendId)
      // friends.value.splice(friendId, 1)
      // we can use splice when we are dealing with index but here we have to deal with friendId

    }

    return {friends, favoriteStatus, addContact, deleteContact}
  },
});
</script>

<style>
</style>
