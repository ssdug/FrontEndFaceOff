<template>
  <div>

    <section class="hero" style="position: relative;">
      <div id="hero-video">
        <video autoplay="" muted="" style="margin: auto; position: absolute; z-index: 5; top: 50%; left: 50%; transform: translate(-50%, -50%); visibility: visible; opacity: 1; width: auto; height: 924px;">
          <!-- <source src="https://chucknorris.com/assets/themes/chuck-norris/videos/chucknorris.mp4" type="video/mp4"> -->
          <source src="../assets/chucknorris.mp4" type="video/mp4">
          <source src="https://chucknorris.com/assets/themes/chuck-norris/videos/chucknorris.webm" type="video/webm">
          <source src="https://chucknorris.com/assets/themes/chuck-norris/videos/chucknorris.ogv" type="video/ogg">
        </video>
      </div>
    </section>

    <div class="toggleRow">
      <div class="rowItem">I <img src="../assets/heart.png" style="width: 20px;"> Autostart Videos - </div>
      <div class="rowItem">
        <div class="toggleButton">
          <div>No&nbsp;</div>&nbsp;
          <toggle-button id="videoSwitch"
                         v-model="videoEnabled"
                         :width="40" :height="20"
                         :color="{checked: 'green', unchecked: 'gray'}" />
          &nbsp;<div>&nbsp;Yes</div>
        </div>
      </div>
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
      if (!val) {
        this.removeVideoElement()
      }
    }
  },

  methods: {
    removeVideoElement () {
      var element = document.getElementById('hero-video')
      if (element) {
        element.parentNode.removeChild(element)
      }
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

  #hero-video {
    position: absolute;
    z-index: 5;
    height: 921.6px;
    top: 0px;
    left: 0px;
    bottom: 0px;
    right: 0px;
    overflow: hidden;
    background-size: cover;
    background-color: transparent;
    background-repeat: no-repeat;
    background-position: 50% 50%;
    background-image: none;
  }
</style>
