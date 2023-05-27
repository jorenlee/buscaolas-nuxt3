<script setup>
// import { mapGetters} from 'vuex';
// // import videojs from 'video.js';
// // import 'video.js/dist/video-js.css';
// // import 'videojs-contrib-hls';
// // import videojs from "video.js";
// // import 'assets/skins/shaka/videojs.min.css';
// // import es from '~/assets/videojs/es';

// export default {
//     props: {
//         source: String,
//         camera_num: Number,
//         chapters: String,
//         triggerSource: String,
//         source_hd: String
//     },
//     data () {
//         return {
//             htmlVideo: '',
//             actionv: null,
//             offsetv: '12'
//         }
//     },
//     // async created() {
//     //     if (process.client) {
//     //         require('~/static/js/nuevo.min.js')
//     //         require('~/assets/videojs/es.js')
//     //     }
//     // },
//     mounted () {
//         var videojs_options = {
//             preload: "auto",
//             playsinline: true,
//             controls: true,
//             fill: true,
//             fluid: true,
//             language: 'es',
//             crossorigin: "anonymous",
//             poster: "https://media-buscaolas.s3.sa-east-1.amazonaws.com/videos/historial_poster.png",
//             sources: [
//                 {
//                     src: this.source,
//                     type: "application/x-mpegURL",
//                     res: "SD",
//                     label: "SD"
//                 }
//             ]
//             }
//         var nuevo_options = {
//                 shareMenu:false,
//                 rateMenu: false,
//                 zoomMenu: true,
//                 zoomInfo: false,
//                 zoomWheel: false,
//                 chapterMarkers:true,
//                 touchControls: {
//                         disableAnimation: true,
//                         doubleTap: true,
//                     },
//                 controlbar: true,
//                 contextMenu: false,
//                 relatedMenu: false,
//                 downloadButton: true
//             };
//         this.$nextTick(() => {
//         this.player = this.$videojs(this.$refs.videoPlayer, videojs_options);
//         this.player.nuevo(nuevo_options);

//         var chapters = [{kind:"chapters", src:this.chapters, srclang:"es"}];
//         this.player.on('loadeddata', function(){
//             this.loadTracks(chapters);
//         });
//         this.player.on('downloadVideo', function(event,data){
//             console.log('descargando video')
//             document.getElementById('modalloading').style.display = "block";
//             const formdata = new FormData();
//             formdata.append('url',data.source);   
//             formdata.append('tiempo',this.currentTime());
//             formdata.append('duracion',this.duration());
//             fetch('https://puerto.buscaolas.cl/descargavideo',{
//                 method: 'POST',
//                 credentials: 'same-origin',
//                 headers:{
//                     'X-Requested-With': 'XMLHttpRequest'
//                 },
//                 mode: 'no-cors',
//                 body: formdata
//                 })
//                 .then(response => {
//                     return {'url':'videocut.mp4'}//response.json()
//                 })
//                 .then(data => {
//                     console.log(data['url'])
//                     const anchor = document.createElement("a");
//                     anchor.href = "https://puerto.buscaolas.cl/static/"+data['url'];
//                     anchor.download = "Buscaolas Video.mp4";
//                     document.body.appendChild(anchor);
//                     anchor.click();
//                     document.body.removeChild(anchor);
//                 })
            
//         });
//         });
//         // document.getElementById('modalloading').style.display = "none";
//     },
//         beforeDestroy() {
//         if (this.player) {
//             this.player.dispose()
//         }
//     },
//     computed: {
//       ...mapGetters(['isAuthenticated', 'loggedInUser', 'IsPremium'])
//     },
//     watch: {
//         source(newSource, oldsource){
//             console.log('cambio a ',newSource)
//             const new_video = {
//                 sources: [
//                     {
//                         src: newSource,
//                         type: "application/x-mpegURL",
//                     },
//                 ]
//             }
//             console.log(this.chapters)
//             var chapters = [{kind:"chapters", src:this.chapters, srclang:"es"}];
//             this.player.on('loadeddata', function(){
//             this.loadTracks(chapters);
//             });
//             this.player.changeSource(new_video)
//         }
//     },
// }
</script>
<template>
    <video ref="videoPlayer" class="video-js vj-fluid">
        <source :src="source" type="application/x-mpegURL" />
    </video>
</template>

