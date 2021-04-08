<template>
  <div>
    <Navbar />
  </div>
  <router-view/>
</template>

<script>
import Navbar from '@/components/Navbar'
export default {
  name: 'App',
  components: {
    Navbar
  }
}
</script>


<style>
/* Font for the city name  font-family: 'Bebas Neue', cursive;*/
@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Raleway:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Raleway', sans-serif;
  background-color: #e6f4f1;
}

#app {
  color: #0d0d0d;
}

ul li {
  list-style: none;
}
</style>
