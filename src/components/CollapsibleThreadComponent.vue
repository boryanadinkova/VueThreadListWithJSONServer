<template>
    <div class="CollapsibleThreadContainer " 
      @click="expand" 
      :class="[{expanded: expandedRows}, thread[0].score > 5 ? 'high-priority' : 'low-priority']"
    >        
        <div class="messageRibbon" v-if="thread[0] && !expandedRows">{{ thread.length }} messages</div>
        <SingleThreadComponent 
          v-for="(item, index) in thread" 
          :key="item.id" 
          :thread="item" 
          :class="[item.score && item.score > 5 ? 'high-priority' : 'low-priority', `message${ index + 1 }`]"
          :style="{'z-index': 2-index}"
          
        >
        </SingleThreadComponent>
    </div>
</template>

<script>

import SingleThreadComponent from './SingleThreadComponent';

export default {
  name: 'CollapsibleThreadComponent',
  components: { SingleThreadComponent },
  data: function() {
    return {
        index: Number, 
        expandedRows: false
    }
  },
  props: {
    thread: {
        type: Array
    }
  },
  methods: {
    expand() {
      this.expandedRows = true;
    }
  },
  computed: {
    test: function(index) {        
        return index;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

@import './../assets/_mixins';
@import './../assets/shared';

.CollapsibleThreadContainer {
    width: 100%;
    min-height: 140px;
    @include setFlexbox($direction: column);
}

.messageRibbon {
    @include dimensions(20%, 20px);
    @include adjust-position(1.5rem, 14.5rem, null, relative);
    @include setFlexbox();
    z-index: 4;
    font-size: 0.7rem;
    border-radius: 8px;
    color: $font-color-ribbon;
}

// Sorry for this :D
@media (max-width: 716px) {
    .messageRibbon {
        left: 13.5rem;
    }
}

@media (max-width: 660px) {
    .messageRibbon {
        left: 11.5rem;
    }
}

@media (max-width: 570px) {
    .messageRibbon {
        left: 9.5rem;
        top: 1.3rem;
    }
}

@media (max-width: 480px) {
    .messageRibbon {
        left: 8.5rem;
    }
}

@media (max-width: 410px) {
    .messageRibbon {
        left: 7.5rem;
        font-size: 0.6rem
    }
}

@media (max-width: 410px) {
    .messageRibbon {
        left: 6.5rem;
        font-size: 0.6rem
    }
}
// Sorry for this :D

.high-priority .messageRibbon {
  background: $highRateMessageRibbon;
}

.low-priority .messageRibbon {
  background: $lowRateMessageRibbon;
}


.message2 {
    margin-top: -107px;
    margin-left: 20px;
}

.message3 {
    margin-top: -107px;
    margin-left: 40px;
}

.expanded .message2,
.expanded .message3 {
    margin-top: 2%;
    margin-left: 0;
    animation: expandRows 0.9s ease-in-out;
}

@keyframes expandRows {
  from {
    margin-top: -107px;
  }
  to {
    margin-top: 2%;
    margin-left: 0;
  }
}

</style>