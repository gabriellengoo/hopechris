<template>
  <!-- <Tutorial/> pt-[12.5rem] pt-[5rem]-->
  <div class="pb-[5rem] pt-[2rem]  pl-[2rem] pr-[2rem]">

    <!-- logo -->
    <div v-if="home && home.sections" class="homeimgsize z-0">
              <div v-for="section in home.sections" :key="section._key" class=''>
                <MediaImage
                  :size="section.image.size"
                  :aspect="section.image.aspect"
                  :src="section.image.image"
                  v-if="section.image.image"
                  class="md:h-[17vw] h-auto object-cover"
                ></MediaImage>
              </div>
            </div>
    <!-- welcome text -->
    <div
      v-for="section in home.sections"
      :key="section._key"
      class="py-5 weltext"
    >
      <Richtext
        class="weltextc"
        :blocks="section.content"
        v-if="section.content"
      ></Richtext>
      <MediaImage
        :src="section.title.title"
        v-if="section.title.title"
        class=""
      ></MediaImage>
    </div>
    <!-- list of archive -->
    <div v-if="home.grid2" class="">
      <Grid2 class="" size="small" :items="home.grid2"></Grid2>
    </div>
  </div>
</template>

<script>
import { groq } from "@nuxtjs/sanity";
import { mapState, mapActions, mapMutations } from "vuex";
// import "@fortawesome/fontawesome-free/css/all.css";
// import Marqueec from "~/components/Marqueec.vue";
// import Vue3Marquee from 'vue3-marquee';
// import AboutPage from '~/components/AboutPage.vue'
// import Header from "~/components/layout/Header.vue";
// import LenisComponent from "~/components/LenisComponent.vue";
// import Lenis from "@studio-freight/lenis";
// import Works from "~/pages/works.vue";
// import Poems from "~/components/Poems.vue";
// import Poems from "~/pages/poems.vue";
// import Home from "~/pages/index.vue";
// import MailchimpForm from "~/components/MailchimpForm.vue";
// import SeatedWidget from "~/components/SeatedWidget.vue";

// import gsap from 'gsap';
// import { ScrollTrigger } from 'gsap/ScrollTrigger';

export default {
  name: "IndexPage",

  components: {
    // Marqueec,
    // LenisComponent,
    // Header,
    // Works,
    // Home,
    // Poems,
    // MailchimpForm,
    // SeatedWidget,
  },

  data() {
    return {
      project: false,
      abouts: [],
      index: 1,
      lenis: null,
      realIndex: 0,
      step: 0,
      isBlueBoxActive: false,
      contentContainerStyle: {},
      scrolled: false,
      back: false,
      abouts: [],
      activeStyle: { textDecoration: "none" },
      isCollapsibleOpen: false,
      isGlitching: false,
      currentSection: "home",
      containerTransform: "translateX(0)",
      newSectionTransform: "translateX(100vw)",
    };
  },

  scroll() {
    if (this.project.slider) {
      this.scrolled = !this.scrolled;
      const gsap = this.$gsap;
      let height = this.$refs["footer"].offsetHeight;
      if (this.scrolled) {
        gsap.to(this.$refs["container"], { y: -height });
      } else {
        gsap.to(this.$refs["container"], { y: 0 });
      }
    }
  },

  async asyncData({ $sanity, store }) {
    const homeQuery = groq`*[_type == "home" ] {..., listImage, linkin, linkst, linkco } {..., 
     
     grid[] {_key, spacer,youtubeUrl,vimeoUrl, "video" : 
    {"id" : video.asset->playbackId, "aspect" : video.asset->data.aspect_ratio},
      "image" : {"image" : image.asset._ref, "aspect" : image.asset->metadata.dimensions.aspectRatio, "position" : position}, 
    title, photographer,year,hair,styleing, link, production, location,
      "reference" : {"key" : reference._ref, "title" : reference->title, "clients" : reference->client[].label, "slug" : reference->slug.current, "talent" : reference->talent->title, "team" : reference->team, "meta" : reference->meta}} } 
     
      {..., grid2[] {_key, spacer, thumdnailTime,youtubeUrl,vimeoUrl, "video" : 
    {"id" : video.asset->playbackId, "aspect" : video.asset->data.aspect_ratio},
      "image" : {"image" : image.asset._ref, "aspect" : image.asset->metadata.dimensions.aspectRatio, "position" : position}, 
    title, dis, photographer,year,imageWidth,hair,makeup,dop,set,styleing, link, production, location, listImage, draft,
      "reference" : {"key" : reference._ref, "title" : reference->title, "dis" : reference->dis, "clients" : reference->client[].label, "slug" : reference->slug.current, "talent" : reference->talent->title, "team" : reference->team, "meta" : reference->meta}} } 
     
      {..., gridm[] {_key, spacer, thumdnailTime,youtubeUrl,vimeoUrl, "video" : 
    {"id" : video.asset->playbackId, "aspect" : video.asset->data.aspect_ratio},
      "image" : {"image" : image.asset._ref, "aspect" : image.asset->metadata.dimensions.aspectRatio, "position" : position}, 
    title, photographer,year,imageWidth,hair,makeup,dop,set,styleing, link, production, location, listImage, draft,
      "reference" : {"key" : reference._ref, "title" : reference->title, "clients" : reference->client[].label, "slug" : reference->slug.current, "talent" : reference->talent->title, "team" : reference->team, "meta" : reference->meta}} } 


    {...,meta[]{
      title,
      content,
    }}

    {...,metaemails[]{
      title,
      content,
      link,
     
    }}


      {...,
        sections[]{
          title,
          subtitle,
          content,
          "title" : {"title" : title.asset._ref, "aspect" : image.asset->metadata.dimensions.aspectRatio, "position" : position}, 
          "image" : {"image" : image.asset._ref, "aspect" : image.asset->metadata.dimensions.aspectRatio, "position" : position}, 
        }
      }


      {...,
        sections2[]{
          title2,
          content2,
        }
      }

      {...,
        sections3[]{
          title3,
          content3,
        }
      }

      {...,
        sections4[]{
          title4,
          youtubeUrl,
          vimeoUrl,
          "video" : 
                    {"id" : video.asset->playbackId, "aspect" : video.asset->data.aspect_ratio},
          "image4" : {"image4" : image4.asset._ref, "aspect" : image4.asset->metadata.dimensions.aspectRatio, "position" : position}, 

        }

        {...,
        sections5[]{
          title5,
          content5,
        }
      }

      {...,
        sections6[]{
          title6,
          content6,
        }
      }

      }
      
      | order(_updatedAt desc)[0]
      `;

    const home = await $sanity.fetch(homeQuery);

    // Commit meta and metaemails to the Vuex store
    // store.commit("setMeta", home.meta);
    // store.commit("setMetaEmails", home.metaemails);
    // store.commit("setThumdnailTime", home.thumdnailTime);
    // store.commit('setYear', home.year);

    return { home };
  },

  //   mounted() {
  //     const lenis = new Lenis()

  // lenis.on('scroll', (e) => {
  //   console.log(e)
  // })

  // function raf(time) {
  //   lenis.raf(time)
  //   requestAnimationFrame(raf)
  // }

  // requestAnimationFrame(raf)

  //   },
  mounted() {
    this.loadData();
  },

  methods: {
    ...mapActions(["fetchPoems"]),
    ...mapActions(["setTitle"]),
    ...mapMutations(["TOGGLE_MENU"]),

    async loadData() {
      await this.fetchPoems();
    },

    handleArrowClick() {
      // Scroll down by 100vh
      window.scrollTo({
        top: window.scrollY + window.innerHeight,
        behavior: "smooth", // for smooth scrolling
      });
    },

    startGlitchEffect() {
      this.isGlitching = true;
      setTimeout(() => {
        this.isGlitching = false;
      }, 1000); // Adjust the duration of the glitch effect
    },

    setProject(reference) {
      this.project = reference;
    },
    toggleCollapsible() {
      this.isCollapsibleOpen = !this.isCollapsibleOpen;
    },

    openGallery() {
      this.$store.commit("setGalleryState", true); // Set gallery state as open
    },
    closeGallery() {
      this.$store.commit("setGalleryState", false); // Set gallery state as closed
    },
    getYouTubeEmdedUrl(youtubeUrl) {
      // Extract YouTube video ID from the URL
      const videoId = youtubeUrl.split("v=")[1];
      // Generate the YouTube emded URL with autoplay, mute, loop, and hide controls on hover parameters
      return `https://www.youtube.com/emded/${videoId}?autoplay=1&mute=1&controls=0&loop=1&showinfo=0`;
    },
    getVimeoEmdedUrl(vimeoUrl) {
      // Extract Vimeo video ID from the URL
      const videoId = vimeoUrl.split("/").pop();
      // Generate the Vimeo emded URL
      return `https://player.vimeo.com/video/${videoId}?autoplay=1&loop=1&autopause=0`;
    },
    toggleBlueBox() {
      // Toggle the blue box visibility
      this.isBlueBoxActive = !this.isBlueBoxActive;

      // Update the content container position
      this.updateContentContainerPosition();

      if (this.isBlueBoxActive) {
        document.body.style.overflow = "hidden";
      } else {
        document.body.style.overflow = "auto";
      }
    },
    updateContentContainerPosition() {
      const isMobile = window.innerWidth <= 768;
      // Calculate the offset based on blue box height
      const offset = isMobile
        ? this.isBlueBoxActive
          ? "100vh"
          : "0"
        : this.isBlueBoxActive
        ? "365px"
        : "0";

      // Calculate the offset based on whether it's a mobile screen or not

      // Set the content container position
      this.contentContainerStyle = {
        transform: `translateY(${offset})`,
      };
    },
    goBack() {
      this.currentSection = "home";
      this.containerTransform = "translateX(0)";
      this.newSectionTransform = "translateX(100vw)";
    },
    transitionToPoems() {
      // Move the container to the left and bring in the Poems section
      this.containerTransform = "translateX(-50vw)";
      this.newSectionTransform = "translateX(0)";
      // Set the current section to 'poems'
      this.currentSection = "poems";
    },
  },
  computed: {
    ...mapState(["menu"]),

    arrowIconClass() {
      // fas fa-arrow-up
      return this.isCollapsibleOpen ? "" : "fas fa-arrow-down";
    },

    ...mapState({
      poems: (state) => state.poems.data,
    }),
  },
  // created() {
  //   this.setTitle(this.home.title);
  // },
};
</script>
