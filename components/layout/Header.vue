<template>
  <div class="p-[2rem] fixed left-15 top-15 1000:top-30 1000:left-30 z-50 serif leading-none  pb-[5rem] text-sm flex w-screen justify-between">
    <!-- text-[1.4rem] -->
    <p class="uppercase">We are the new hope</p>
    <div class="uppercase">
      <NuxtLink to="/" class="p-10 header-link">Store</NuxtLink>
      <NuxtLink to="/">Contact</NuxtLink>
    </div>
  </div>
</template>

<script>
import { mapState, mapMutations } from "vuex";

export default {
  data() {
    return {
     
    };
  },
  methods: {
    ...mapMutations(["TOGGLE_MENU"]),

 
  },
  computed: {
    ...mapState(["menu"]),

    arrowIconClass() {
      return this.isCollapsibleOpen ? "fas fa-arrow-up" : "fas fa-arrow-down";
    },
  },
};
</script>


<style scoped>
a{
  /* cursor: url('/CURSOR.svg'), auto !important; */
  text-decoration: none;
  color: black;
  opacity: .3;
  /* animation: bounce 1s infinite alternate; */
  transition-duration: .5s;
}

a:hover{
  opacity: 1;
  transition-duration: .5s;
}

.abouttexttitle {
  text-transform: uppercase;
  font-family: "Roboto", sans-serif;
  font-weight: 900;
}

.containerhome {
  display: flex;
  width: 200vw; /* Double the width for both sections */
  height: 100vh;
  transition: transform 0.5s ease-in-out;
  overflow: hidden;
}

.new-section {
  width: 50vw;
  height: 100vh;
  transition: transform 0s ease-in-out;
  overflow: hidden;
}

.presssectextlink {
  /* padding-top: 1rem; */
  text-transform: uppercase;
  font-family: "Roboto", sans-serif;
  font-weight: 900;
}
</style>
