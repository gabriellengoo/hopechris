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
      <div
        v-masonry-tile
        class="relative transition-opacity duration-300 item"
        v-for="item in items"
        :key="item._key"
        :class="[
          item.double ? 'double h-fit' : '',
          item.spacer != 0 ? '' : '',

        ]"
      >
      
        <figure
          class="flex flex-col w-[19vw]"
          :style="{ minHeight: item.video.id ? (isDesktop ? 'auto' : 'auto') : 'auto' }"
          :class="[
            item.spacer
              ? `h-space-${item.spacer + 1} md:h-space-${item.spacer}`
              : item.image.aspect >= 1
              ? item.double
                ? 'h-space-10 md:h-space-10 2xl:h-space-10'
                : 'h-space-5 md:h-space-3 2xl:h-space-2'
              : item.double
              ? 'h-space-fit md:h-space-fit 2xl:h-space-fit'
              : 'h-space-12 md:h-space-6 2xl:h-space-4',
          ]"
        >
          <figure
            :class="[
              containerClass,
              item.image.position == 'right'
                ? 'items-end'
                : item.image.position == 'center'
                ? 'items-center'
                : 'items-start',
            ]"
          >
            <span class="flex flex-col items-start w-auto h-full max-w-full">
              <section class="relative z-10 grid md:grid-cols-12 grid-cols-2 gap-y-18 1000:gap-y-12 1000:px-30 1000:pb-50 pt-150 1000:pt-125 w-full max-w-2000 mx-auto">
                <section class="col-span-11 1000:col-span-12 select-none">
                  <div class="grid  md:grid-cols-12 grid-cols-2 gap-x-10 1000:gap-y-10 1000:gap-x-36">
                    <p v-if="item.dis" class="col-span-2 1000:col-span-1 sans whitespace-nowrap opacity-30 text-sm">
                      {{ item.dis }}
                    </p>
                    <div class="1000:leading-20 pb-2 col-span-10 1000:max-w-[500px] serif richT">
                      <a v-if="item.youtubeUrl" :href="item.youtubeUrl" target="_blank">
                        <figcaption class="text-sm" v-if="size == 'small'">
                          <span v-if="item.title">{{ item.title }}</span>
                          <span v-else>{{ item.reference.title }}</span>
                        </figcaption>
                      </a>
                      <MediaImage
                        :size="item.image.size"
                        :aspect="item.image.aspect"
                        :src="item.image.image"
                        v-if="item.image.image"
                        :class="imageClass"
                        :sizes="size == 'sm' ? 'sm:60vw md:15vw' : 'sm:150vw md:150vw'"
                      ></MediaImage>
                      <a v-if="item.vimeoUrl" :href="item.vimeoUrl" target="_blank">
                        <figcaption class="text-sm" v-if="size == 'small'">
                          <span v-if="item.title">{{ item.title }}</span>
                          <span v-else>{{ item.reference.title }}</span>
                        </figcaption>
                      </a>
                      <!-- Display YouTube Video -->
                      <iframe
                        v-if="item.vimeoUrl"
                        :src="getYouTubeEmbedUrl(item.vimeoUrl)"
                        frameborder="0"
                        allowfullscreen
                        class="w-[80vw] md:w-auto"
                      ></iframe>
                    </div>
                  </div>
                </section>
              </section>
            </span>
          </figure>
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
      project: false,
      containerClass: 'flex flex-col w-full h-full',
      imageClass: 'contain-image',
      isDesktop: false,
    };
  },
  computed: {
    ...mapState(['activeProject', 'activeTalent']),
  },
  mounted() {
    this.redraw();
    this.isDesktop = window.innerWidth > 768;
    window.addEventListener('resize', this.handleResize);
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.handleResize);
  },
  methods: {
    ...mapMutations(['SET_ACTIVE_PROJECT', 'SET_ACTIVE_TALENT']),
    redraw() {
      if (typeof this.$redrawVueMasonry === 'function') {
        this.$redrawVueMasonry();
      }
    },
    getYouTubeEmbedUrl(vimeoUrl) {
      const videoId = vimeoUrl.split("v=")[1];
      return `https://www.youtube.com/embed/${videoId}?autoplay=1&mute=1&controls=0&loop=1&showinfo=0`;
    },
    handleResize() {
      this.isDesktop = window.innerWidth > 768;
    },
    hover(item) {
      if (item.reference.title) {
        this.SET_ACTIVE_PROJECT(item.reference);
        if (this.size === 'small') {
          this.SET_ACTIVE_TALENT(item.reference);
        } else {
          this.SET_ACTIVE_TALENT(item.reference.talentId);
        }
      } else {
        this.SET_ACTIVE_PROJECT(false);
      }
    },
    leave() {
      this.SET_ACTIVE_PROJECT(false);
      this.SET_ACTIVE_TALENT(false);
    },
  },
};
</script>

<style scoped>
a:hover {
  text-decoration: underline;
}

.vdpadoverview {
  padding: 5px;
}
</style>
