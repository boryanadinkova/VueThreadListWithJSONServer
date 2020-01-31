<template>
    <div class="threadContainer">
        <div class="headerSection threadSection">
            <div class="subject" :class="getPriority > 5 ? 'high-priority' : 'low-priority'">{{ getSingleThread.subject }}</div>
            <div class="team">{{ getSingleThread.team }}</div>
        </div>
        <div class="questionSection threadSection">
            <div class="question">{{ getSingleThread.question }}</div>
            <div class="createdAt">{{ getSingleThread.created_at | moment("MMM Do") }}</div>
        </div>
        <div class="textSection threadSection">{{ getSingleThread.text }}</div>
    </div>
</template>

<script>

export default {
  name: 'SingleThreadComponent',
  data: function() {
    return {
        message: {},
        score: Number
    }
  },
  props: {
    thread: {
        type: Object
    },
    data: {
        type: Object
    }
  },
  computed: {
    getSingleThread: function() {
        if (this.thread === undefined) {
            return;
        }
        let message = this.thread;
        
        return message;
    },
    getPriority: function() {
        let score = this.getSingleThread.score
        return score
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

@import './../assets/_mixins';
@import './../assets/shared';

.threadContainer {
    @include dimensions(94%, 100px);
    @include setFlexbox($justify: space-around, $direction: column);
    margin: 2% 0%;
    background: $messageBackground;
    border-radius: 5px;
    box-shadow: 6px 2px 39px -10px $boxShadowColor1;

    .threadSection {
        width: 90%;
        @include setFlexbox($justify: space-between);
    }

    .headerSection {
        height: 30%;
        align-items: flex-end;

        .subject {
            width: 49%;
            font-weight: map-get($font-weights, "bold");
        }

        .team {
            width: 45%;
            text-align: end;
            font-weight: map-get($font-weights, "regular");
        }
    }

    .questionSection {
        height: 30%;
        align-items: flex-start;
        font-size: 0.7rem;
        font-weight: map-get($font-weights, "bold");

        .question {
            width: 75%;
            align-self: flex-start;
        }

        .createdAt {
            width: 20%;
            align-self: flex-start;
            text-align: end;
        }
    }

    .textSection {
        height: 30%;
        align-items: flex-start;
        font-size: 0.8rem;
        font-weight: 600;
    }
    
    .high-priority {
        color: $highRateHeader;
    }

    .low-priority {
        color: $lowRateHeader;
    }
}


@media ($max-w-768) {
    
    .threadContainer {
      @include dimensions(96%, 100px);
      margin: 1.8% 0%;

      .threadSection {
          width: 92%;
      }

      .questionSection {
          font-size: 0.65rem;
          height: 50%;  
      }

      .textSection {
          height: 18%;
          font-size: 0.7rem;
      }
    }    
}

@media ($max-w-319) {
  
    .threadContainer {
        @include dimensions(94%, 90px);
    }    
  }

</style>