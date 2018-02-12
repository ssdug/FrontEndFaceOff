<template>
  <div>
    <section class="hero" style="position: relative;">
      <div id="hero-video" style="position: absolute; z-index: 5; top: 0px; left: 0px; bottom: 0px; right: 0px; overflow: hidden; background-size: cover; background-color: transparent; background-repeat: no-repeat; background-position: 50% 50%; background-image: none;">
        <video autoplay="" muted="" style="margin: auto; position: absolute; z-index: 5; top: 50%; left: 50%; transform: translate(-50%, -50%); visibility: visible; opacity: 1; width: auto; height: 924px;">
          <source src="https://chucknorris.com/assets/themes/chuck-norris/videos/chucknorris.mp4" type="video/mp4">
          <source src="https://chucknorris.com/assets/themes/chuck-norris/videos/chucknorris.webm" type="video/webm">
          <source src="https://chucknorris.com/assets/themes/chuck-norris/videos/chucknorris.ogv" type="video/ogg">
        </video>
      </div>
    </section>
    <div class="videoControls">
      <div>Show Video</div>
    </div>
    <div class="videoControls">
      <div>Off&nbsp;</div>&nbsp;
      <toggle-button id="videoSwitch"
                     v-model="videoEnabled"
                     :width="40" :height="20"
                     :color="{checked: 'green', unchecked: 'gray'}" />
      &nbsp;<div>&nbsp;On</div>
    </div>
  </div>
</template>

<script>
import Cookies from 'js-cookie'

export default {
  name: 'Video',
  data () {
    return {
      msg: '',
      videoEnabled: this.getVideoCookie()
    }
  },

  watch: {
    videoEnabled: function (val) {
      Cookies.set('showVid', val)
    }
  },

  methods: {
    removeVideoElement () {
      var element = document.getElementById('hero-video')
      element.parentNode.removeChild(element)
    },

    getVideoCookie () {
      let cookie = Cookies.get('showVid')

      // the cookie doesn't exist so create one and set to show the video
      if (cookie === undefined) {
        Cookies.set('showVid', true)
        return true
      } else if (cookie === 'true') {
        return true
      } else {
        return false
      }
    }

  },

  mounted () {
    let vm = this

    if (vm.videoEnabled) {
      setTimeout(function () { vm.removeVideoElement() }, 12800)
    } else {
      vm.removeVideoElement()
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .videoControls {
    display: flex;
    justify-content: flex-end;
    align-content: center;
    padding-right: 20px;
  }

  #hero-video {
    height: 921.6px;
    /*z-index: 5 !important;*/
  }

</style>
