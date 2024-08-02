<template>
  <div class="header-container fixed left-4 top-4 z-50 serif leading-none pb-20 text-sm w-[90%] md:w-[98%] flex flex-col md:items-start items-center 1000:flex-row 1000:justify-between 1000:items-center">
    <p class="header-title ">We are the new hope</p>
    <div class="header-links flex flex-col  uppercase 1000:mt-0 1000:flex-row  1000:space-x-4">
      <NuxtLink to="https://www.facebook.com/ChisaraMusic/" class="p-2">Store</NuxtLink>
      <NuxtLink to="/" class="p-2">Contact</NuxtLink>
    </div>
  </div>
</template>
<script>
import { mapState, mapMutations } from "vuex";

export default {
  data() {
    return {};
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
a {
  text-decoration: none;
  color: black;
  opacity: 0.3;
  transition-duration: 0.5s;
}

a:hover {
  opacity: 1;
  transition-duration: 0.5s;
}

.header-container {
  padding: 1rem;
}

.header-title {
  /* font-size: 2rem; */
  text-transform: uppercase;
}

.header-links {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 1rem;
}

.header-link {
  padding: 0.5rem;
}

@media (min-width: 1000px) {
  .header-container {
    /* padding: 2rem; */
    /* left: 2rem; */
    top: 2rem;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }

  .header-title {
  /* font-size: 2rem; */
  text-transform: uppercase;
}

  .header-links {
    flex-direction: row;
    margin-top: 0;
    gap: 1rem;
    align-items: flex-end;
  }

  .header-link {
    padding: 1rem;
  }
}
</style>
