<style lang="scss">
  @import '~@/abstracts/_variables.scss';

  div#add-cafe-button{
    background-color: $secondary-color;
    width: 56px;
    height: 56px;
    border-radius: 50px;
    -webkit-box-shadow: 0 2px 2px 0 rgba(0,0,0,0.14), 0 3px 1px -2px rgba(0,0,0,0.12), 0 1px 5px 0 rgba(0,0,0,0.2);
    box-shadow: 0 2px 2px 0 rgba(0,0,0,0.14), 0 3px 1px -2px rgba(0,0,0,0.12), 0 1px 5px 0 rgba(0,0,0,0.2);
    text-align: center;
    z-index: 9;
    cursor: pointer;
    position: absolute;
    right: 60px;
    bottom: 30px;
    color: white;
    line-height: 50px;
    font-size: 40px;
  }
</style>

<template>
  <div id="add-cafe-button" v-on:click="checkAuth()">
    &plus;
  </div>
</template>

<script>
  import { EventBus } from '../../event-bus.js';

  export default {
    computed: {
      /*
        Retrieves the User from Vuex
      */
      user(){
        return this.$store.getters.getUser;
      },

      /*
        Retrieves the User Load Status from Vuex
      */
      userLoadStatus(){
        return this.$store.getters.getUserLoadStatus();
      }
    },

    methods: {
      checkAuth(){
        if( this.user == '' && this.userLoadStatus == 2 ){
          EventBus.$emit('prompt-login');
        }else{
          this.$router.push({ name: 'newcafe'});
        }
      }
    }
  }
</script>
