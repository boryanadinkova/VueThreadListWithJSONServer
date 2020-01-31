<template>
  <div id="app">
    <ThreadsComponent :data="this.threads"></ThreadsComponent>
  </div>
</template>

<script>
import axios from "axios";
import ThreadsComponent from './components/ThreadsComponent.vue';

export default {
  name: "app",
  components: {ThreadsComponent},
  data() {
    return {
      threads: []
    };
  },
  async created() {
    try {
      const res = await axios.get(`http://localhost:3000/threads`);
      this.threads = res.data;
    } catch (e) {
      console.log(e);
    }
  }
};
</script>

<style lang="scss">

@import './assets/_mixins';
@import './assets/shared';

html, body {
  @include dimensions(100%, null);
  @include setFlexbox();
  background: $background;
  margin: 0;
  padding: 0;
  min-height: min-content;
  flex: 1;
  overflow: auto;
}

#app {
  @include dimensions();
  @include setFlexbox($direction: column);
  font-family: $font;
  color: $font-color; 
  font-size: $font-size; 
}

@media ($max-w-768) {

  #app {
    font-size: $font-size - 1; 
  }
}

@media ($max-w-319) {
    
  #app {
    font-size: $font-size - 1; 
    overflow-x:scroll;
  }
}
</style>
