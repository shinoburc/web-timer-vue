<template>
  <div id="webtimer">
    <div id="count" class="card">
      <div class="card-header timer-header">
        <button type="button" class="btn btn-primary btn-lg" v-on:click="start">
          <i class="fas fa-play">&nbsp;</i> Start
        </button>
        <button type="button" class="btn btn-danger btn-lg" v-on:click="stop">
          <i class="fas fa-stop">&nbsp;</i> Stop
        </button>
        <button type="button"  class="btn btn-secondary btn-lg" v-on:click="clear">
          <i class="fas fa-trash-alt">&nbsp;</i> Clear
        </button>
      </div>
      <div class="card-body timer-body">
        <div class="input-group">
          <input type="number" class="form-control timer-control" placeholder="00" max="99" min="0" v-model.number="hour">
          <div>:</div>
          <input type="number" class="form-control timer-control" placeholder="00" max="59" min="0" v-model.number="minute">
          <div>:</div>
          <input type="number" class="form-control timer-control" placeholder="00" max="59" min="0" v-model.number="second">
        </div>
      </div>
      <div class="card-footer timer-footer">
        <button type="button" class="btn btn-primary btn-lg" v-on:click="plus10m">
          <i class="fas fa-plus">&nbsp;</i> 10 m
        </button>
        <button type="button" class="btn btn-primary btn-lg" v-on:click="plus10s">
          <i class="fas fa-plus">&nbsp;</i> 10 s
        </button>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'WebTimer',
  data() {
    return {
      timer: undefined,
      hour: 0,
      minute: 0,
      second: 0,
      audio: new Audio("sound/Mallet.ogg"),
    }
  },
  computed: {
    current_timer_seconds: function () {
      return (this.hour * 60 * 60) + (this.minute * 60) + (this.second);
    }
  },
  methods: {
    start: function () {
      this.timer = setInterval(() => {
        var current_timer_seconds = this.current_timer_seconds;
        if(current_timer_seconds == 0){
          this.audio.play();
          return;
        }
        current_timer_seconds -= 1;
        this.hour = parseInt( current_timer_seconds / (60 * 60) );
        this.minute = parseInt( (current_timer_seconds % (60 * 60)) / 60 );
        this.second = parseInt( current_timer_seconds  % 60 );
      }, 1000)
    },
    stop: function () {
      if(typeof this.timer !== "undefined") {
        clearInterval(this.timer);
      }
      this.audio.pause();
    },
    clear: function () {
      this.stop();
      this.hour = 0;
      this.minute = 0;
      this.second = 0;
    },
    plus10m: function () {
      if( this.minute + 10 <= 59 ) {
        this.minute += 10;
      }
    },
    plus10s: function () {
      if( this.second + 10 <= 59 ) {
        this.second += 10;
      }
    },
  },
  created() {
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.timer-header {
  text-align: center;
}
.timer-body {
  text-align: center;
  font-size: 20vw;
}
.timer-footer {
  text-align: center;
}
.timer-control {
  text-align: center;
  font-size: 20vw;
}
input[type=number]::-webkit-inner-spin-button, 
input[type=number]::-webkit-outer-spin-button {  
     opacity: 1;
}
</style>
