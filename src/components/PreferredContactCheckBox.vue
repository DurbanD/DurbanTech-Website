<template>
  <div class="pref-contact-selector">
    <input
    class="pref-checkbox"
    type="checkbox"
    :checked="value"
    @change="$emit('input', $event.target.checked)"
    :value="name" >
    <p class="pref-label">{{ label }}</p>
  </div>
</template>

<script>
import { Vue } from 'vue-property-decorator'

const PreferredContactCheckBox = Vue.extend({
  props: {
    label: String,
    name: String,
    value: Boolean
  }
})
export default PreferredContactCheckBox
</script>

<style>
.pref-contact-selector {
  width: 90%;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: flex-start;
  padding: 0;
  margin: 0;
  height: auto;
}
.pref-label {
  color: var(--font-dark);
  padding: 2px 5px;
}
</style>
