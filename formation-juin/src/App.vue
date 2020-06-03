import { default } from './views/Home.vue';
<template>
  <div id="app">
    <we-cursor-provider path="dam/asset">
      <template #default="cursor">
        <div>
          <dam-search :cursor="cursor"/>
          <dam-list :cursor="cursor"/>
        </div>
      </template>
    </we-cursor-provider>
  </div>
</template>

<script>
  import DamList from '@/components/dam/DamList'
  import DamSearch from '@/components/dam/DamSearch'

  export default {
  components: {
    DamList,
    DamSearch
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
