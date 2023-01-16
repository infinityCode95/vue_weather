<template>
  <div class="app-wrap">
    <Header/>
    <Content/>
  </div>
</template>

<script>
import Header from '@/components/Header';
import Content from '@/components/Content';

export default {
  name: 'App',
  components: {
    Header,
    Content
  },
  data: () => ({
    
  }),
  computed: {

  },
  methods: {
  
  }
}
</script>

<style lang="css">
#app {
  font-family: Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

.app-wrap {
  width: 90vw;
  padding: 1rem;
}

.error-text {
  color: red;
}
</style>
