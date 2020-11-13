<template>
  <div id="app">
    <div id="nav">
    </div>
    <router-view />
    <Footer />
  </div>
</template>

<script>
import Footer from '@/components/Footer.vue'

export default {
  components: {
    Footer
}
}
</script>