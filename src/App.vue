<template>
  <form @submit.prevent="submit">
    <my-input name="Username"
      :rules="{ required: true, min: 5 }"
      :value="username.value"
      :error="username.error"
      @update="update"
    />

    <my-input name="Password"
      :rules="{ required: true, min: 10 }"
      type="password"
      :value="password.value"
      :error="password.error"
      @update="update"
    />

    <my-checkbox
      :checked="terms.value"
      :error="terms.error"
      @change="change"
    
    />

    <my-button
      background="darkslateblue"
      color="white"
      :disabled="!valid"
    />
  </form>
</template>

<script >
// import HelloWorld from './components/HelloWorld.vue'
  import MyButton from './components/MyButton.vue';
  import MyInput from './components/MyInput.vue';
  import MyCheckbox from './components/MyCheckbox.vue';

export default{
  components:{
    MyButton,
    MyInput,
    MyCheckbox
  },

  data(){
    return{
      username: {
        value: 'user',
        error: ''
      },
      password: {
        value: 'pass',
        error: ''
      },
      terms : {
        value: false,
        error: ''
      }
    }
  },

  computed: {
    valid(){
      return(
        !this.username.error &&
        !this.password.error &&
        this.terms.error
      )
    }
  },

  methods: {
    update({name, value, error}){ // events raise from child component to parent
      // this.username.value = value;
      this[name].value = value
      this[name].error = error
    },
    change({checked, error}){
      this.terms.value = checked;
      this.terms.error = error;
      // console.log('i dey here' + checked);
    },
    submit($){
      console.log('Event');
    }
  }
}

</script>

<style scoped>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
</style>
