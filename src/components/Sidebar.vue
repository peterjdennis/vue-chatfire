<template>

  <div class="sidebar">
    <h1 class="ui inverted center aligned header">#Tutox::Stacks</h1>
    <connected-user></connected-user>
    <channels></channels>
  </div>

</template>


<script>
   import ConnectedUser from './sidebar/ConnectedUser'
   import Channels from './sidebar/Channels'
  export default{

  name: 'sidebar',

  components: {
      ConnectedUser, Channels
  }

  }


</script>

<style scope>
  .sidebar{
  position: fixed;
  display: flex;
  flex-flow: column nowrap;
  width: 300px;
  padding: 10px;
  top: 0;
  left: 0;
  bottom: 0;
  background-color: #795548;
  padding-top: 110px;
  }


</style>
