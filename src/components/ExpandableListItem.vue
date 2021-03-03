<template>
  <li class="li-component-main" v-on:click="expandableItemClick" v-bind:class="{ li_expanded:expand }">
    <h3 class="li-component-head">{{ messageMain }}</h3>
    <p v-if="expand" class="li-component-expand">
      {{ messageExpanded }}
    </p>
    <p v-if="expand" class="li-back">
      {{ backMessage }}
    </p>
  </li>
</template>

<script>
import { Vue } from 'vue-property-decorator'
const ExpandableListItem = Vue.extend({
  data () {
    return {
      expand: false,
      backMessage: 'Click to go back.'
    }
  },
  props: {
    messageMain: String,
    messageExpanded: String
  },
  methods: {
    expandableItemClick: function (event) {
      const otherComponents = event.target.parentElement.parentElement.querySelectorAll('.li-component-main')
      if (!this.expand) {
        for (const C of otherComponents) if (C !== event.target.parentElement && C !== event.target) C.style.display = 'none'
        this.expand = true
      } else if (this.expand) {
        for (const C of otherComponents) C.style.display = 'flex'
        this.expand = false
      }
    }
  }
})
export default ExpandableListItem
</script>

<style scoped>
.li-component-main {
  padding: 3px 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  justify-items: center;
  align-items: center;
  align-content: center;
}
.li-component-expand  {
  padding: 0;
  margin: 0;
}

.li-component-head {
  list-style: none;
  list-style-position: inside;
  padding: 3px 0;
  margin: 0;
  font-size: 13pt;
  font-weight: normal;
  width: 100%;
  text-align: center;
  padding: 3px 0;
}

.li-component-main:hover, .li_expanded {
  background: var(--primary-light-verytransparent);
  border: 2px solid var(--secondary-dark);
  border-radius: 2px;
}

.li_expanded {
  border: 2px solid var(--secondary-dark);
  border-radius: 3px;
  padding: 10px 5px;
}

.li-back {
  color: var(--primary);
}

.li-back:hover {
  cursor: pointer;
}
</style>
