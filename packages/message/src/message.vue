<template>
  <div>
    <popup v-model="value" position="top" :class="customClass" :modal="false">
      <p>{{ message }}</p>
    </popup>
  </div>
</template>
<style>
  .mint-message {
    width: 100%;
    height: 50px;
    line-height: 50px;
    text-align: center;
    background-color: rgba(0,0,0,.7);
    backface-visibility: hidden;
    opacity: 0.9;
  }
  .mint-message-success {
    background-color: green !important;
  }
  .mint-message-warning {
    background-color: yellow !important;
  }
  .mint-message-info {
    background-color: #fff !important;
  }
  .mint-message-error {
    background-color: red !important;
  }
</style>
<script type="text/babel">
  import Popup from '../../popup';

  export default {
    components: {
      Popup
    },
    data() {
      return {
        duration: 3000,
        timer: null,
        value: false,
        type: '',
        callback: null,
        message: '',
        customClass: {
          type: String,
          default: null
        }
      };
    },
    watch: {
      type(val) {
        console.log(val);
        if (val !== '') {
          this.customClass = `mint-message mint-message-${val}`;
        }
      }
    },
    methods: {
      close() {
        var callback = this.callback;
        this.value = false;
        this.$emit('input', false);
        this.closeTimer();
        setTimeout(() => {
          callback();
        }, 1000);
      },

      closeTimer() {
        clearTimeout(this.timer);
      },

      startTimer() {
        if (this.duration > 0) {
          this.timer = setTimeout(() => {
            if (this.value) {
              this.close();
            }
          }, this.duration);
        }
      }
    },
    mounted() {
      this.startTimer();
    }
  };
</script>
