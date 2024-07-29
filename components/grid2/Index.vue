<template>
  <client-only>

    <!-- logo -->
    <!-- wwelcome first text-->
    <!-- archive by most recent -->


    <div
      v-masonry
      column-width=".item"
      item-selector=".item"
      class="w-full masonry"
      :class="size"
      horizontal-order="true"
    > 
    <!-- item.double ? 'double h-fit' : '', vid height?  --> 
      <div
        v-masonry-tile
        class="relative transition-opacity duration-300 item"
        v-for="item in items"
        :key="item._key"
        :class="[
          item.double ? 'double h-fit' : '',
          item.spacer != 0 ? '' : '',
          item.image.image || item.video.id ? '' : 'hidden md:block',
          // mobile test?
          item.double && size == 'small' ? '' : '',
          activeTalent &&
          activeTalent != item.reference.talentId &&
          activeTalent != item.reference
            ? ''
            : '', 
        ]"
      > 
      <!--  :style="{ backgroundColor: item.double ? 'red' : 'blue', }" 
                  :style="{ minHeight: item.video.id ? (isDesktop ? (item.double ? '75vh' : '45vh') : '15vh') : 'auto' }"
       ? 'h-space-fit md:h-space-fit 2xl:h-space-fit' vid space height--> 
        <figure
          class="flex flex-col w-[19vw]" 
          :style="{ minHeight: item.video.id ? (isDesktop ? 'autoh' : 'auto') : 'auto' }"
          :class="[
            item.spacer
              ? `h-space-${item.spacer + 1}  md:h-space-${item.spacer}`
              : item.image.aspect >= 1
              ? item.double
                 ? 'h-space-10 md:h-space-10 2xl:h-space-10'
                : 'h-space-5 md:h-space-3 2xl:h-space-2'
              : item.double
              ? 'h-space-fit md:h-space-fit 2xl:h-space-fit'
              : 'h-space-12 md:h-space-6 2xl:h-space-4',
              // mb-6
            size == 'small' ? '' : '',
          ]"
        >
          <NuxtLink
            :class="[
              containerClass,
              item.image.position == 'right'
                ? 'items-end'
                : item.image.position == 'center'
                ? 'items-center'
                : 'items-start',
            ]"
            v-if="item.reference.slug"
            :to="`/work/${item.reference.slug}`"
            @mouseenter.native="hover(item)"
            @mouseleave.native="leave()"
          >
            <span
              class="flex flex-col items-start h-full max-w-full"
              :class="size == 'small' ? 'w-full' : 'w-auto'"
            >
              <figure
              class="figsize"
                :class="size == 'small' ? 'block w-full' : 'h-full w-auto'"
                :style="
                  item.video && item.video.aspect && size == 'small'
                    ? `aspect-ratio: ${item.video.aspect.replace(':', '/')}`
                    : ''
                "
              >
                <MediaImage
                  :size="item.image.size"
                  :aspect="item.image.aspect"
                  :src="item.image.image"
                  v-if="item.image.image"
                  class="contain-image"
                  :sizes="
                    size == 'sm' ? 'sm:60vw md:15vw' : 'sm:150vw md:150vw'
                  "
                ></MediaImage>
                <!-- :style="{ backgroundColor: item.double ? 'red' : 'blue', }"  -->
                <MediaVideo 
                  :id="item.video.id"
                  :thumbTime="item.video.thumbTime"                 
     v-if="item.video.id"
                  class="dubvid vdpadoverview object-contain object-top w-auto h-full"
                    
                ></MediaVideo>
              </figure>
              <figcaption
                class="capplace font-bold block  mr-auto "
                v-if="size == 'small'"
              >
                <span v-if="item.title">{{ item.title }}</span>
                <span v-else>{{ item.reference.title }}</span>
              </figcaption>
              <figcaption
                class="capplaces text-center block  mr-auto "
                v-if="size == 'small'"
              >
                <span v-if="item.dis">{{ item.dis }}</span>
                <span v-else>{{ item.reference.dis }}</span>
              </figcaption>
            </span>
          </NuxtLink>
          <a
            v-else-if="item.link"
            :href="item.link"
            target="_blank"
            :class="[
              containerClass,
              item.image.position == 'right'
                ? 'items-end'
                : item.image.position == 'center'
                ? 'items-center'
                : 'items-start',
            ]"
            @mouseenter="
              item.reference.title
                ? SET_ACTIVE_PROJECT(item.reference)
                : SET_ACTIVE_PROJECT(item._key)
            "
            @mouseleave="SET_ACTIVE_PROJECT(false)"
          >
            <span class="flex flex-col items-start w-auto h-full max-w-full">
              <MediaImage
                :size="item.image.size"
                :aspect="item.image.aspect"
                :src="item.image.image"
                v-if="item.image.image"
                class="contain-image"
                :sizes="size == 'sm' ? 'sm:60vw md:15vw' : 'sm:150vw md:150vw'"
              ></MediaImage>
              <MediaVideo
                :id="item.video.id"
                :style="`aspect-ratio: ${item.video.aspect.replace(':', '/')}`"
                v-if="item.video.id"
                :thumbTime="item.video.thumbTime"
                class="object-contain vdpadoverview object-top w-auto h-full"
              ></MediaVideo>


              <div class="flex ">
             <div>texts</div>

              <a v-if="item.youtubeUrl" :href="item.youtubeUrl" target="_blank">
              <figcaption
                class="capplace block py-2 text-sm"
                v-if="size == 'small'"
              >
                <span v-if="item.title">{{ item.title }}</span>
                <span v-else>{{ item.reference.title }}</span>
              </figcaption>
              </a>
            </div>

            </span>
          </a>
          <figure
            v-else
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
       



              <section class="relative z-10 grid grid-cols-12 gap-y-18 1000:gap-y-12 1000:px-30 1000:pb-50 pt-150 1000:pt-125 w-full max-w-2000 mx-auto">
              <section class="col-span-11 1000:col-span-12 select-none">
              <div class="grid grid-cols-12 gap-x-10 1000:gap-y-10 1000:gap-x-36 ">
             <p v-if="item.dis" class="col-span-2 1000:col-span-1 sans whitespace-nowrap opacity-30 text-sm">{{item.dis}}</p>

             <div class="1000:leading-20 pb-2 col-span-10 1000:max-w-[500px] serif richT">
              <a v-if="item.youtubeUrl" :href="item.youtubeUrl" target="_blank">
              <figcaption
                class=" text-sm"
                v-if="size == 'small'"
              >
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
              <figcaption
                class=" text-sm"
                v-if="size == 'small'"
              >
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
              class=""
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
import { mapMutations, mapState } from 'vuex'
export default {
  props: ['items', 'size'],
  data() {
    return {
      project: false,
      containerClass: 'flex flex-col w-full h-full',
      imageClass: 'contain-image',
      isDesktop: false,
    }
  },
  computed: {
    ...mapState(['activeProject', 'activeTalent']),
  },
  mounted() {
    this.redraw()
      // Check if the window width is greater than a certain threshold for desktop
      this.isDesktop = window.innerWidth > 768; // Adjust the threshold as needed
    // Listen to window resize events to update the isDesktop flag
    window.addEventListener('resize', this.handleResize);
  },
  beforeDestroy() {
    // Remove the resize event listener when the component is destroyed
    window.removeEventListener('resize', this.handleResize);
  },

  methods: {
    ...mapMutations(['SET_ACTIVE_PROJECT', 'SET_ACTIVE_TALENT']),
    redraw() {
      if (typeof this.$redrawVueMasonry === 'function') {
        this.$redrawVueMasonry()
      }
    },
    getYouTubeEmbedUrl(vimeoUrl) { 
      // Extract YouTube video ID from the URL
      const videoId = vimeoUrl.split("v=")[1];
      // Generate the YouTube embed URL with autoplay, mute, loop, and hide controls on hover parameters
      return `https://www.youtube.com/embed/${videoId}?autoplay=1&mute=1&controls=0&loop=1&showinfo=0`;
    },
    beforeDestroy() {
    // Remove the resize event listener when the component is destroyed
    window.removeEventListener('resize', this.handleResize);
  },
    hover(item) {
      if (item.reference.title) {
        this.SET_ACTIVE_PROJECT(item.reference)
        if (this.size == 'small') {
          this.SET_ACTIVE_TALENT(item.reference)
        } else {
          this.SET_ACTIVE_TALENT(item.reference.talentId)
        }
      } else {
        this.SET_ACTIVE_PROJECT(false)
      }
    },
    leave() {
      this.SET_ACTIVE_PROJECT(false)
      this.SET_ACTIVE_TALENT(false)
    },
  },
}
</script>
<style scoped>
/* @media (min-width: 768px){
  .masonry.large .item.double {
    height: 55vh;
 
}
} */
 a:hover{
  text-decoration: underline;
 }

.vdpadoverview{
  padding: 5px;
}

</style>