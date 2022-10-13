<template>
  <div id="app">
    <div class="wrapper-swicthes">
      <Swicthes
        v-for="swicth in swicthes"
        :key="swicth.id"
        :swicth="swicth"
      />
    </div>
    <div class="wrapper-hosts">
      <Hosts 
        v-for="host in hosts"
        :key="host.id"
        :host="host"
      />
    </div>
    <!-- <div id="wrapper-line-left"></div> -->
    
  </div>
</template>

<script>
import Swicthes from "./component/Swicthes.vue"
import Hosts from "./component/Hosts.vue"
export default {
  name: 'App',
  components: {
    Swicthes,
    Hosts
  },
  data() {
    return {
      swicthes: [
      {
        id: 1,
        idHost: [19321383, 2232134, 33241, 423423]
      },
      {
        id: 2,
        idHost: [2232134, 634234235, 7656456456, 8324234]
      },
      {
        id: 3,
        idHost: [423423, 33241, 8324234]
      },
      {
        id: 4,
        idHost: [2232134, 54363634, 94324224234234]
      },
      {
        id: 5,
        idHost: [19321383, 33241, 54363634]
      },
    ],
    hosts: [
      {id: 19321383},
      {id: 2232134},
      {id: 33241},
      {id: 423423},
      {id: 54363634},
      {id: 634234235},
      {id: 7656456456},
      {id: 8324234},
      {id: 94324224234234},
    ]
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
#app {
  /* padding: 20px 40px; */
  position: relative;
}
.wrapper-swicthes{
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}

.wrapper-hosts {
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  
}

#wrapper-line-left {
  position: absolute;
  height: 100%;
  width: 1px;
  top: 0;
  left: 200px;
  background-color: blue;
}
</style>
