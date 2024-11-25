<template>
  <client-only>
    <div
      v-masonry
      column-width=".item"
      item-selector=".item"
      class="w-full masonry"
      :class="size"
      horizontal-order="true"
    >
    <div>
      <div class=" bord">
          <p class="w-[6vw]">
            Date
          </p>
          <figcaption class="text-sm">
            Title
          </figcaption>
        </div>
    </div>
      <div
        v-masonry-tile
        class="relative transition-opacity duration-300 item liststyle"
        v-for="item in items"
        :key="item._key"
        :class="[
          item.double ? 'double h-fit' : '',
          item.spacer != 0 ? '' : '',
        ]"
        @mouseenter="hover(item)"
        @mouseleave="leave"
      >
        <div class="list-content">
          <p v-if="item.dis" class="w-[6vw]">
            {{ item.dis }}
          </p>
          <figcaption v-if="item.title" class="text-sm">
            {{ item.title }}
          </figcaption>
        </div>
<!--      v-if="hoveredItem === item" -->
        <figure
     
          class="absolute top-0 left-0 w-full h-full flex flex-col imgspan"
        >
          <MediaImage
            v-if="item.image.image"
            :size="item.image.size"
            :aspect="item.image.aspect"
            :src="item.image.image"
            :class="imageClass"
            :sizes="size == 'sm' ? 'sm:60vw md:15vw' : 'sm:150vw md:150vw'"
            class="imgspanimg"
          ></MediaImage>
          <iframe
            v-if="item.vimeoUrl"
            :src="getYouTubeEmbedUrl(item.vimeoUrl)"
            frameborder="0"
            allowfullscreen
            class="w-full h-full imgspanvid"
          ></iframe>
        </figure>
      </div>
    </div>
  </client-only>
</template>


<script>
import { mapMutations, mapState } from 'vuex';
export default {
  props: ['items', 'size'],
  data() {
    return {
      hoveredItem: null, // State to track the hovered item
      isDesktop: false,
      containerClass: 'flex flex-col w-full h-full',
      imageClass: 'contain-image',
    };
  },
  methods: {
    getYouTubeEmbedUrl(vimeoUrl) {
      const videoId = vimeoUrl.split("v=")[1];
      return `https://www.youtube.com/embed/${videoId}?autoplay=1&mute=1&controls=0&loop=1&showinfo=0`;
    },
    hover(item) {
      this.hoveredItem = item; // Set the currently hovered item
    },
    leave() {
      this.hoveredItem = null; // Clear the hovered item on mouse leave
    },
  },
};

</script>

<style scoped>
.bord{
  border-bottom: .02vw solid #1C1C1C;
  padding-bottom: .5vw;
    padding-top: .5vw;
    display: flex;
    position: relative;
}

.liststyle {
  width: 100%;
  border-bottom: .02vw solid #1C1C1C;
  /* padding-top: 2vw; */
  color: #1C1C1C;
  background-color: rgba(0, 0, 0, 0);
  position: relative;
  /* transition: .5s ease-in-out; */
}

.liststyle:hover {
color: rgb(234, 234, 234);
 background-color: #1C1C1C;
 z-index: 100 !important;
 z-index: 100 !important;
    position:fixed;
    width: 100vw;
    left: 0;
 /* transition: .5s ease-in-out; */
}

.list-content {
  padding-bottom: .5vw;
    padding-top: .5vw;
    display: flex;
    position: relative;
}

.list-content:hover {
  background-color: #1C1C1C;
  padding-bottom: .5vw;
    padding-top: .5vw;
    display: flex;
    z-index: 100 !important;
    position: relative;
}

figure {
  transition: opacity 0.3s ease-in-out;
  opacity: 0;
}

.liststyle:hover figure {
  opacity: 1;
  z-index: 90;
}

.imgspan{
  position: fixed;
    z-index: 90;
    display: flex;
    justify-content: center;
    align-items: center;
    pointer-events: none;
    width: 100vw;
    height: 100vh !important;
    top: 0;
    left: 0;
    background-color: #ffffff;
}

.imgspanimg img{
  width: 40vw;
  width: 40vw;
    height: 10vw;

  /* position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);  */
}

.masonry .item img {
    width: 40vw !important;
    z-index: 90 !important;
}

figure iframe{
  z-index: 90;
  width: 100vw;
    height: 100vh;
}
</style>

