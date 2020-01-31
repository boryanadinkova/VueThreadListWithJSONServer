<template>
    <div class="threadsContainer">
      <div class="messageContainer" v-for="thread in data" :key="thread.id" > 
        <CollapsibleThreadComponent v-if="thread.length > 1" :thread="thread"></CollapsibleThreadComponent>
        <SingleThreadComponent v-else :thread="thread[0]"></SingleThreadComponent>
      </div>
    </div>
</template>

<script>

import SingleThreadComponent from './SingleThreadComponent.vue';
import CollapsibleThreadComponent from './CollapsibleThreadComponent.vue';

export default {
  name: 'ThreadsComponent',
  components: { CollapsibleThreadComponent, SingleThreadComponent }, 
  data: function() {
    return {
        transformedData: [],
    }
  },
  props: {
    data: Array
  }
}
</script>

<style scoped lang="scss">

  @import './../assets/_mixins';
  @import './../assets/shared';

  .threadsContainer {
      @include dimensions(768px, 100%);
      @include setFlexbox($direction: column, $justify: space-evenly);
      flex-grow: 1; 

      .messageContainer {
        @include dimensions(94%, null);
        @include setFlexbox($justify: space-around, $direction: column);
      }
  };

  @media ($max-w-768) {
    
    .threadsContainer {
      @include dimensions();
    }
  }

  @media ($max-w-319) {
  
    .threadsContainer {
      @include dimensions(320px, 100%);
      overflow-y: auto;
      overflow-x: hidden;
      transform-origin: right top;
    }    
  }
</style>