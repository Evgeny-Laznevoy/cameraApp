<template>
    <div class="camera">
        <video autoplay class="camera__feed"></video>
        <button @click="clickPicture" class="camera__snap">SNAP</button>
    </div>
</template>

<script>
export default {
    name: "camera",
    methods: {
        init() {
            if ('mediaDevices' in navigator && 'getUserMedia' in navigator.mediaDevices) {
                     let constraints = {
                       video: {
                           width: {
                               min: 640,
                               ideal: 1280,
                               max: 1920
                           },
                           height: {
                               min: 360,
                               ideal: 720,
                               max: 1080
                           }
                       }
                   }
               navigator.mediaDevices.getUserMedia(constraints).then(stream =>{
                   const videoPlayer = document.querySelector("video")
                   videoPlayer.srcObject = stream
                   videoPlayer.play()
               }) 
            } else {
                alert('cannot get Media Devices')
            }
        },
        clickPicture(){
            this.$emit('takePicture')
        }
    },
    beforeMount(){
        this.init()
    }
}
</script>

<style lang="scss" scoped>
    .camera {
        height: 1000px;
        width: 100vw;
        box-sizing: border-box;
        padding: 25px;
        
        &__feed {
            display: block;
            width: 100%;
            max-width: 1280px;
            box-shadow: 4px 4px 12px 0px rgba($color: #000000, $alpha: .4); 
            background-color: #000000;
            margin: 0 auto;
        }

        &__snap {
            display: block;
            height: 50px;
            margin: 0 auto;
            margin-top: 100px;
            border-radius: 50%;
            background-color: transparentize($color: #7ea534, $amount: .7);
            cursor: pointer;
            border: 1px solid #000000;
            outline: none;

            &:hover {
               background-color: transparentize($color: #7ea534, $amount: .4); 
            }

            &:active {
                background-color: transparentize($color: #7ea534, $amount: .1);
            }
        }
    }
</style>