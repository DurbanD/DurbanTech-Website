<template>
  <div class="about-box">
    <h2 class="about-box-head">{{ head }}</h2>
    <ul class="about-list">
      <li is="ExpandableListItem" v-for="listItem in listItems"
       :key='listItem.main'
        v-bind:messageMain="listItem.main"
         :messageExpanded="listItem.expanded"
         class="about-list-item" />
    </ul>
  </div>
</template>

<script>
import { Vue } from 'vue-property-decorator'
import ExpandableListItem from '../components/ExpandableListItem'

const AboutBox = Vue.extend({
  props: {
    head: String,
    listItems: Array
  },
  components: {
    ExpandableListItem
  }
})
export default AboutBox
</script>

<style scoped>
h1 {
  margin: 0;
  padding: 0;
  justify-self: flex-start;
}
h2 {
  margin: 0;
  padding: 0;
}
h3 {
  margin: 0;
  padding: 0;
}
p {
  margin: 0;
  margin-bottom: 0.5rem;
  padding: 1rem 0;
  border-bottom: 1px dotted var(--lightgreen-transparent);
}
ul {
  padding: 0;
  margin: 0;
  list-style: none;
  list-style-position: inside;
}
ul {
  text-align: left;
  margin-top: 0.5rem;
}
.about-box {
  padding: 1rem 0;
  width: 100%;
}
</style>
