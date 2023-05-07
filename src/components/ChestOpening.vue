<template>
    <div class="hello">
        <div class="openingBar">
            <h1>Picking Lock...</h1>
        </div>
    </div>
  </template>
  
  <script>
  export default {
   
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
    .openingBar{
        position: absolute;
  left: 50%;
  top: 65%;
  margin-left: -175px;
  /* -1/2 width */
  margin-top: -175px;
  /* -1/2 height */
        width: 350px;
        height: 50px;
        border: solid black 5px;
    }
 
  </style>
  