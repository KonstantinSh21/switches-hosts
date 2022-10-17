<template>
    <div :id="`host${host.id}`" class="host">
        host {{host.id}}
    </div>
  </template>
  
  <script>
  export default {
    name: 'Hosts',
    props: {
        host: Object,
    },
  }
  </script>
  
  <style>
  .host {
    position: relative;
    width: 100px;
    height: 100px;
    border: 3px solid #000;
    margin: 20px 0;
    border-radius: 50%;
    box-sizing: border-box;
    background: #000;
    align-items: center;
    color: red;
    z-index: 4;
  }

  </style>
  