<script setup>
// // import { mapGetters} from 'vuex';
// export default {
// //   middleware: 'auth',
//   data() {
//     return {
//       filterBy: null,
//       DataFiltered: null
//     }
//   },
//   async asyncData({ $axios, params}) {
//       const VideosData  = await $axios.$get(
//         "/api/main/playa/history/puntalobos"
//       );
//       return { VideosData };
//   },
//   computed: {
//     //   ...mapGetters(['isAuthenticated', 'loggedInUser', 'IsPremium']),
//     //     filterData(){
//     //     if(this.filterBy){
//     //     this.DataFiltered = this.VideosData.videos.filter((list) => {
//     //       return list.date.match(this.filterBy)
//     //     });
//     //       return this.DataFiltered 
//     //     } else {
//     //       return this.VideosData.videos
//     //     }
//     //   }
//     },
// };
</script>
<template>
  <div>
    <div class="flex flex-col">
      <div class="md:w-9/12 mx-auto lg:pt-16 w-full grid lg:grid-cols-2">
        <div><VideoHistory :source="VideosData.videos[0].url_video" :chapters="VideosData.videos[0].url_chapters" /></div>
        <div> <VideoHistory :source="VideosData.videos[0].url_video_primium" :chapters="VideosData.videos[0].url_chapters_premium" v-if="VideosData.videos[0].url_video_primium" /></div>
      </div>
    </div>
  </div>
</template>



<style lang="scss" scoped>
.vjs-touch-inactive:not(.vjs-scrubbing):not(.vjs-ad-playing) .vjs-control-bar {
  opacity: 1 !important;
  pointer-events: all !important;
}
</style>
