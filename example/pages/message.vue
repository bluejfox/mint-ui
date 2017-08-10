<template>
  <div class="page-message">
    <div class="page-title">Message</div>
    <div class="page-msg-wrapper">
      <mt-button @click.native="showMessage('success')" size="large">显示成功消息</mt-button>
      <mt-button @click.native="showMessage('warning')" size="large">显示警告消息</mt-button>
      <mt-button @click.native="showMessage('info')" size="large">显示正常消息</mt-button>
      <mt-button @click.native="showMessage('error')" size="large">显示错误消息</mt-button>
    </div>
  </div>
</template>
<style>
  @component-namespace page {
    @component msg {
      @descendent wrapper {
        padding: 0 20px;
        position: absolute 50% * * *;
        width: 100%;
        transform: translateY(-50%);
        button:not(:last-child) {
          margin-bottom: 20px;
        }
      }
    }
  }
</style>
<script type="text/babel">
  import { Message } from 'src/index';

  export default {
    methods: {
      showMessage(type) {
        Message[type](type);
      }
    }
  };
</script>
