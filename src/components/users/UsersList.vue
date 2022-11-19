<template>
  <button @click="confirmInput">Confirm</button>
  <button @click="saveChanges">Save Changes</button>
  <ul>
    <user-item v-for="user in users" :key="user.id" :name="user.fullName" :role="user.role"></user-item>
  </ul>
</template>

<script>
import UserItem from './UserItem.vue';

export default {
  components: {
    UserItem,
  },
  inject: ['users'],
  data() {
    return {
      changeSaved: false
    }
  },
  methods: {
    confirmInput() {
      this.$router.push('/teams')
    },
    saveChanges() {
      this.changeSaved = true
    }
  },
  beforeRouteLeave(to, from, next) {
    if(this.changeSaved){
      next()
    }else {
      const userWantsToLeave = confirm('are u sure?')
      next(userWantsToLeave)
    }
  }
  // beforeRouteEnter(to, from, next) {

  // }
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 2rem auto;
  max-width: 20rem;
  padding: 0;
}
</style>