<template>
  <div class="link-item">
    <router-link class="link-item-cover" :to="to">
      <div class="bg" :style="bg"></div>
    </router-link>

    <router-link class="link-item-text" :to="to">{{ text }}</router-link>
  </div>
</template>

<script>
export default {
  name: 'LinkItem',
  data () {
    return {
      bg: 'background-image:url(' + this.src + ')'
    }
  },
  props: {
    to: String,
    src: String,
    text: String
  }
}
</script>
