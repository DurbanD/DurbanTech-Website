<template>
  <div class="info-hover" v-on:mouseover="mouseHover" v-on:mouseout="mouseLeavesBox">
    <p id="info-hover-main-display">{{ iconInnerText }}</p>
    <p id="info-hover-text" v-if="showInfoText" :style="{ left:`${innerTextLeftPos}px`, top:`${innerTextTopPos}px` }" >{{ hoverText }}</p>
  </div>
</template>

<script>
import { Vue } from 'vue-property-decorator'
const InfoHover = Vue.extend({
  data () {
    return {
      hoverTextID: 'hover-text-container',
      innerHoverTextID: 'hover-inner-text',
      iconInnerText: '?',
      innerTextTopPos: 0,
      innerTextLeftPos: 0,
      showInfoText: false
    }
  },
  props: {
    hoverText: String
  },
  methods: {
    mouseHover (event) {
      this.innerTextTopPos = event.clientY
      this.innerTextLeftPos = event.clientX
      this.showInfoText = true
    },
    mouseLeavesBox () {
      this.showInfoText = false
    }
  },
  computed: {
  }
})
export default InfoHover
</script>

<style scoped>
.info-hover {
  border-radius: 50%;
  border: 1px solid black;
  padding: 0;
  margin: 0 0.5rem;
  background: var(--primary-light-transparent);
}
#info-hover-main-display {
  padding: 2px 5px;
  margin: 0;
}
#info-hover-text {
  position: absolute;
  background: var(--secondary-light-semisolid);
  padding: 3px 8px;
  border: 1px solid black;
  border-radius: 4px;
}
</style>
