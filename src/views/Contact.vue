<template>
  <div class="contact">
    <div id="contact-head" v-if="!formSubmitted">
      <h1 id='contact-container-headText'>{{ headerTextLarge }}</h1>
      <p id='contact-container-subText'>{{ headerTextSmall }}</p>
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
      formSubmitted: false,
      headerTextLarge: 'Contact',
      headerTextSmall: 'Use the form below or email DurbanTech at admin@durbantech.com. We will get back to you as soon as we can!'
    }
  },
  components: {
    ContactForm
  },
  computed: {
    // Computed Values
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
#contact-head {
  margin: 0.5rem;
  color: var(--font-light);
}
p {
  margin:0;
  padding: 0;
  margin-bottom: 0;
}
h1 {
  margin: 0.5rem 0;
  padding:0;
}

@media screen and (max-height: 850px) {
  #contact-container-subText {
    display: none;
  }
  #contact-container-headText {
    margin: 0;
    padding: 0;
    font-size: 18pt;
  }
}
@media screen and (max-height: 750px) {
  #contact-head {
    display: none;
  }
}
</style>
