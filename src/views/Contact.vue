<template>
  <div class="contact">
    <div class="contact-head" v-if="!formSubmitted">
      <h1>Contact</h1>
      <p v-if="!isLessThan700Height">Use the form below or email DurbanTech at admin@durbantech.com</p>
    </div>
    <ContactForm v-on:form-submit-success="formSubmitted = true" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import ContactForm from '@/components/ContactForm.vue'

@Component({
  data () {
    return {
      formSubmitted: false
    }
  },
  components: {
    ContactForm
  },
  computed: {
    isLessThan700Height () {
      if (document.body.clientHeight < 700) return true
      return false
    },
    isLessThan500Height () {
      if (document.body.clientHeight < 500) return true
      return false
    }
  }
})
export default class Contact extends Vue {}
</script>

<style scoped>
.contact {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: var(--secondary-deep-verytransparent) !important;
  margin: 0;
  padding: 0;
}
.contact-head {
  margin: 0.5rem;
  color: var(--font-light);
}
p {
  margin:0;
  padding: 0;
  margin-bottom: 0;
}
h1 {
  margin:0;
  padding:0;
  margin-bottom: 0.5rem;
}

@media screen and (max-height: 850px) {
  p {
    display: none
  }
  h1 {
    margin-bottom: 0;
    font-size: 16pt;
  }
}
@media screen and (max-height: 750px) {
  /* h1 {
    display: none;
  } */
  .contact-head {
    margin: 0 0 0.5rem 0;
  }
}
</style>
