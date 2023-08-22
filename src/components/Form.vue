<template>
  <form @submit.prevent="onSubmit">
    <b>Name: </b>
    <input type="text" v-model="name" required> <br>
    <b>Email: </b>
    <input type="text" v-model="email" required> <br>
    <b>Age: </b>
    <input type="number" v-model="age" required> <br>
    <b>Phone Number: </b>
    <input type="text" v-model="phone_num" required> <br>
    <b>Date of Birth: </b>
    <input type="date" v-model="dob" required> <br>
    <b>Address: </b>
    <input type="text" v-model="address" required> <br>
    <button type="submit" :disabled="isLoading || !isValidEmail">Submit</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      isLoading: false,
      name: '',
      email: '',
      age: '',
      phone_num: '',
      dob: '',
      address: '',
    }
  },
  computed: {
    isValidEmail() {
      const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
      return emailPattern.test(this.email)
    },
  },
  methods: {
    onSubmit() {
      this.isLoading = true

      this.$socket.emit('log-response', {
        name: this.name,
        email: this.email,
        age: this.age,
        phone_num: this.phone_num,
        dob: this.dob,
        address: this.address,
      })
      this.isLoading = false
    },
  },
  // mounted() {
  //   this.$socket.on('user-connected', socketId => {
  //     this.snackbar.text = socketId
  //     this.snackbar.visible = true
  //   })
  // },
}
</script>
