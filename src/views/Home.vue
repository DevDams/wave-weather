<template>
  <div class="home">
    <!-- <Weather /> -->
    <Mobile />
  </div>
</template>

<script>
// @ is an alias to /src
// import Weather from '@/components/Weather.vue'
import Mobile from '@/components/Mobile.vue'

export default {
  name: 'Home',
  components: {
    // Weather,
    Mobile
  }
}
</script>
