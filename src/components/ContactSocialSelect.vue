<template>
  <div>
    <label>{{ label }}</label>
    <select id="contact-select">
      <option v-for="opt in optionList" :key="opt.key" :value="opt.value">{{ opt.name }}</option>
    </select>
  </div>
</template>

<script>
import { Vue } from 'vue-property-decorator'

const ContactSocialSelect = Vue.extent({
  props: {
    label: String,
    optionList: Array
  }
})
export default ContactSocialSelect
</script>