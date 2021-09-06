<script>
import Vue from 'vue';
import BrainedLogin from '@/brained-login.vue';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    BrainedLogin
  }
});
</script>

<template>
  <div id="app">
    <brained-login />
  </div>
</template>
