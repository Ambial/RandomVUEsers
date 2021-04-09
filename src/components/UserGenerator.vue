<template>
  <img
    v-bind:src="picture"
    :alt="`${firstName} ${lastName}`"
    :class="gender"
  />
  <h1>{{firstName}} {{lastName}}</h1>
  <h3>{{email}}</h3>
  <button 
    :class="this.gender"
    @click="getUser"
    >Generate User</button>
</template>

<script>
export default {
  name: 'home',
  props: {
    msg: String
  },
  data() {
    return {
      firstName: 'John',
      lastName: 'Doe',
      email: 'john@gmail.com',
      gender: 'male',
      picture: 'https://randomuser.me/api/portraits/men/10.jpg',
    }
  },
  methods: {
    async getUser() {
      const res = await fetch('https://randomuser.me/api')
      const { results } = await res.json()

      this.firstName = results[0].name.first
      this.lastName = results[0].name.last
      this.email = results[0].email
      this.gender = results[0].gender
      this.picture = results[0].picture.large
    },
  },
}
</script>

<style>

</style>