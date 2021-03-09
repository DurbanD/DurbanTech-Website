<template>
    <form @submit.prevent="onSubmit" id="contact-form" name="form-contact-main" data-netlify=true method="post" action="">

      <!-- Netlify Form Submission Handling -->
      <input type="hidden" name="form-name" value="form-contact-main" />
      <input type="hidden" name="contact-name" />
      <input type="hidden" name="contact-preferred" />
      <input type="hidden" name="contact-phone" />
      <input type="hidden" name="contact-email" />
      <input type="hidden" name="contact-other" />
      <input type="hidden" name="contact-message" />
      <input type="hidden" name="form-content" />

      <!-- Name Input -->
      <FormGroup v-model="form.name"
      v-if="!formSubmitted"
      label="Name"
      type="text"
      placeholder="Full Name"
      class="contact-group"
      id="contact-group-name"
      v-bind:errorStatus="formErrorStatus.name"
      v-bind:errorMessage="formErrorMsg.name" />

      <!-- Contact Selector (Phone | Email | Other) -->
      <div id="contact-selector-main" v-if="!formSubmitted">
        <div id="contact-selector-head">
          <h3><span v-if="formErrorStatus.contact" class="form-error-span">{{ errorMarkerText }}</span>{{ contactSelectHead }}</h3>
          <InfoHover hoverText="1 or more required" />
        </div>
        <div id="contact-selector-container">
          <div
          id="phone-selector"
          class="contact-selector"
          v-on:click="selectContact"
          :class="{ activeSelector: contactSelect.phone, validatedInput : phoneIsValid }">
            <span v-if="phoneIsValid" class="contact-input-confirmed">&#10003;</span>
            {{ contactSelectTextPhone }}
          </div>
          <div
          id="email-selector"
          class="contact-selector"
          v-on:click="selectContact"
          :class="{ activeSelector: contactSelect.email, validatedInput : emailIsValid }">
            <span v-if="emailIsValid" class="contact-input-confirmed">&#10003;</span>
            {{ contactSelectTextEmail }}
          </div>
          <div
          id="other-selector"
          class="contact-selector"
          v-on:click="selectContact"
          :class="{ activeSelector: contactSelect.other, validatedInput : socialIsValid }">
          <span v-if="socialIsValid" class="contact-input-confirmed">&#10003;</span>
            {{ contactSelectTextOther }}
          </div>
        </div>
      </div>

      <!-- Phone Contact Input -->
      <div class="contactContainer" v-if="!formSubmitted && contactSelect.phone">
        <PreferredContactCheckBox
        id="phone-contact-preferred"
        v-model="form.contact.preferred.phone"
        v-if="!formSubmitted && contactSelect.phone"
        label="Set phone as preferred contact"
        name="phone" />
        <FormGroup v-model="form.contact.phone"
        v-if="!formSubmitted && contactSelect.phone"
        label="Phone Number"
        type="tel"
        placeholder="(555) 123 - 4567"
        class="contact-group"
        id="contact-group-phone"
        v-bind:errorStatus="formErrorStatus.phone"
        v-bind:errorMessage="formErrorMsg.phone" />
      </div>

      <!-- Email Contact Input -->
      <div class="contactContainer" v-if="!formSubmitted && contactSelect.email">
        <PreferredContactCheckBox
        id="email-contact-preferred"
        v-model="form.contact.preferred.email"
        v-if="!formSubmitted && contactSelect.email"
        label="Set email as preferred contact"
        name="email" />
        <FormGroup v-model="form.contact.email"
        v-if="!formSubmitted && contactSelect.email"
        label="Email Address"
        type="email"
        placeholder="example@email.com"
        class="contact-group"
        id="contact-group-email"
        v-bind:errorStatus="formErrorStatus.email"
        v-bind:errorMessage="formErrorMsg.email" />
      </div>

      <!-- Social/Other Contact Input -->
      <div class="contactContainer" v-if="!formSubmitted && contactSelect.other">
        <PreferredContactCheckBox
        id="social-contact-preferred"
        v-model="form.contact.preferred.social"
        v-if="!formSubmitted && contactSelect.other"
        label="Set social as preferred contact"
        name="social"  />
        <div id="social-contact-form">
          <div id="service-select">
            <FormGroup v-model="form.contact.social.service"
            v-if="!formSubmitted && contactSelect.other"
            type="opt"
            class="contact-group"
            id="contact-group-social-service"
            :errorStatus="formErrorStatus.social"
            :errorMessage="formErrorMsg.social"
            :optionList="[
              {name: 'LinkedIn', value: 'linkedin'},
              {name: 'Twitter', value: 'twitter'},
              {name: 'Instagram', value: 'instagram'},
              {name: 'Facebook', value: 'facebook'},
              {name: 'Discord', value: 'discord'},
              {name: 'Element', value: 'element'},
              {name: 'Other', value: 'other'},

            ]" />

            <input v-if="form.contact.social.service==='other' && contactSelect.other && !formSubmitted"
            v-model="form.contact.social.namedService"
            id="other-contact-input"
            placeholder="Service Name" >
          </div>

          <FormGroup v-model="form.contact.social.name"
          v-if="!formSubmitted && contactSelect.other"
          type="text"
          placeholder="Username or ID"
          class="contact-group"
          id="contact-group-social-name"
          :errorStatus="formErrorStatus.social"
          :errorMessage="formErrorMsg.social" />
        </div>
      </div>

      <!-- Message Input -->
      <FormGroup v-model="form.message"
      v-if="!formSubmitted"
      label="Message"
      type="textarea"
      placeholder="Your message here..."
      class="contact-group"
      id="contact-group-message"
      v-bind:errorStatus="formErrorStatus.message"
      v-bind:errorMessage="formErrorMsg.message" />

      <!-- Submit Area & Button -->
      <div v-if="!formSubmitted" class="contact-group" id="submit-btn-group">
        <button type="submit" class="btn" id="submit-btn">{{ submitBtnText }}</button>
      </div>
      <div v-if="formSubmitted" id="form-submit-success">
        <h1 id="form-success-head">{{ successHead }}</h1>
        <p id="form-success-body">{{ successBody }}</p>
      </div>
    </form>
</template>

<script>
import { Vue } from 'vue-property-decorator'
import FormGroup from '../components/FormGroup'
import PreferredContactCheckBox from '../components/PreferredContactCheckBox'
import InfoHover from '../components/InfoHover'

const ContactForm = Vue.extend({
  data () {
    return {
      form: {
        name: '',
        message: '',
        contact: {
          phone: '',
          email: '',
          social: {
            service: '',
            namedService: '',
            name: ''
          },
          preferred: {
            phone: false,
            email: false,
            social: false
          }
        }
      },
      formSubmitted: false,
      formErrorStatus: {
        name: false,
        phone: false,
        email: false,
        message: false,
        social: false,
        contact: false
      },
      formErrorMsg: {
        name: 'Name is required',
        phone: '10 Digits - (555) 123 - 1234',
        email: 'example@email.com',
        message: 'Message is required',
        social: 'Service name and contact ID'
      },
      contactSelect: {
        phone: true,
        email: false,
        other: false,
        social: false
      },
      contactSelectHead: 'Contact Type',
      contactSelectTextPhone: 'Phone',
      contactSelectTextEmail: 'Email',
      contactSelectTextOther: 'Other',
      checkmarkConfirm: '&#10003;',
      errorMarkerText: '*',
      submitBtnText: 'Send',
      successHead: 'Thanks!',
      successBody: 'Form successfully submitted.'
    }
  },
  methods: {
    encode (data) {
      return Object.keys(data).map(
        key => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`
      ).join('&')
    },
    postFormDataWithFetch () {
      const headers = { 'Content-Type': 'application/x-www-form-urlencoded' }
      const method = 'POST'
      const body = this.encode({
        'form-name': 'form-contact-main',
        'contact-name': this.form.name,
        'contact-preferred': this.preferredContactString,
        'contact-phone': this.phoneContactString,
        'contact-email': this.emailContactString,
        'contact-other': this.socialContactString,
        'contact-message': this.form.message,
        'form-content': this.contactFormString
      })
      fetch('/', {
        method: method,
        headers: headers,
        body: body
      }).catch(err => alert(err))
    },
    onSubmit () {
      this.setFormErrorStatus()
      if (this.formIsValid) {
        console.log('Valid Form Submission')
        this.formSubmitted = true
        this.$emit('form-submit-success')
        this.postFormDataWithFetch()
      } else if (!this.formIsValid) {
        console.log('Invalid Form Submission')
      }
      console.log(this.contactFormString)
    },
    selectContact (event) {
      const id = event.srcElement.id
      switch (id) {
        case 'phone-selector':
          this.setContactSelect('phone')
          break
        case 'email-selector':
          this.setContactSelect('email')
          break
        case 'other-selector':
          this.setContactSelect('other')
          break
        default:
          break
      }
    },
    setContactSelect (type) {
      for (const contactKey of Object.keys(this.contactSelect)) {
        if (contactKey === type) this.contactSelect[contactKey] = true
        else if (contactKey !== type) this.contactSelect[contactKey] = false
      }
    },
    setFormErrorStatus () {
      if (this.contactIsValid) {
        this.formErrorStatus.email = false
        this.formErrorStatus.phone = false
        this.formErrorStatus.social = false
        this.formErrorStatus.contact = false
      } else if (!this.contactIsValid) {
        this.formErrorStatus.email = true
        this.formErrorStatus.phone = true
        this.formErrorStatus.social = true
        this.formErrorStatus.contact = true
      }
      this.nameIsValid ? this.formErrorStatus.name = false : this.formErrorStatus.name = true
      this.messageIsValid ? this.formErrorStatus.message = false : this.formErrorStatus.message = true
      this.contactIsValid ? this.formErrorStatus.contact = false : this.formErrorStatus.contact = true
    },
    setErrorMsg (type, string) {
      switch (type) {
        case 'message':
          this.formErrorMsg.message = string
          break
        case 'phone':
          this.formErrorMsg.phone = string
          break
        case 'email':
          this.formErrorMsg.email = string
          break
        case 'name':
          this.formErrorMsg.name = string
          break
        default:
          return false
      }
    }
  },
  computed: {
    formIsValid () {
      return (
        this.nameIsValid && this.contactIsValid && this.messageIsValid
      )
    },
    nameIsValid () {
      return this.form.name.length > 0
    },
    messageIsValid () {
      if (this.form.message.length < 1) {
        this.setErrorMsg('message', 'Message required')
        return false
      }
      if (this.form.message.length < 10) {
        this.setErrorMsg('message', '10 or more characters required')
        return false
      }
      return true
    },
    emailIsValid () {
      if (this.form.contact.email.length < 1) return false
      const regEx = /[A-Z0-9._%+-]+@[A-Z0-9.-]+.[A-Z]{2,4}/igm
      return regEx.test(this.form.contact.email)
    },
    phoneIsValid () {
      if (this.form.contact.phone.length < 1) return false
      const regEx = /^\(?\d{3}\)? ?-? ?\d{3} ?-? ?\d{4}$/
      return regEx.test(this.form.contact.phone)
    },
    socialIsValid () {
      if (this.form.contact.social.service.length < 1 || this.form.contact.social.name < 1) return false
      if (this.form.contact.social.service === 'other' && this.form.contact.social.namedService.length < 1) return false
      return true
    },
    contactIsValid () {
      if (this.socialIsValid || this.phoneIsValid || this.emailIsValid) return true
      return false
    },
    phoneContactString () {
      const prefStatus = this.form.contact.preferred.phone
      if (!this.phoneIsValid) return ''
      return `${prefStatus === true ? '(*) ' : ''}${this.form.contact.phone}`
    },
    emailContactString () {
      const prefStatus = this.form.contact.preferred.email
      if (!this.emailIsValid) return ''
      return `${prefStatus === true ? '(*) ' : ''}${this.form.contact.email}`
    },
    socialContactString () {
      const prefStatus = this.form.contact.preferred.social
      const service = this.form.contact.social.service
      const namedService = this.form.contact.social.namedService
      const name = this.form.contact.social.name
      if (!this.socialIsValid) return ''
      return `${prefStatus === true ? '(*) ' : ''}Service Name: ${service !== 'other' ? service : namedService} - Service ID: ${name}`
    },
    preferredContactString () {
      const socialPrefStatus = this.form.contact.preferred.social
      const emailPrefStatus = this.form.contact.preferred.email
      const phonePrefStatus = this.form.contact.preferred.phone
      let preferredString = ''
      if (!socialPrefStatus && !emailPrefStatus && !phonePrefStatus) return preferredString + 'None'
      if (socialPrefStatus) preferredString += 'Social'

      if (emailPrefStatus) {
        if (socialPrefStatus) preferredString += ', '
        preferredString += 'Email'
      }

      if (phonePrefStatus) {
        if (emailPrefStatus || socialPrefStatus) preferredString += ', '
        preferredString += 'Phone'
      }
      return preferredString
    },
    contactFormString () {
      const prefString = this.preferredContactString
      const socialString = this.socialContactString
      const emailString = this.emailContactString
      const phoneString = this.phoneContactString
      const name = this.form.name
      const message = this.form.message

      return `
Name: ${name.length > 0 ? name : 'None'}
Preferred: ${prefString}
Phone: ${phoneString.length > 0 ? phoneString : 'None'}
Email: ${emailString.length > 0 ? emailString : 'None'}
Other: ${socialString.length > 0 ? socialString : 'None'}
Message: ${message.length > 0 ? message : 'None'}
`
    }
  },
  components: {
    FormGroup,
    PreferredContactCheckBox,
    InfoHover
  }
})
export default ContactForm
</script>

<style scoped>
#contact-form {
    width: 100%;
    background: radial-gradient(150% 80%, var(--primary-light-semitransparent), var(--primary-light-transparent)), var(--grey-transparent);
    border: 2px solid black;
    border-radius: 10px;
    padding: 0.5rem 1rem;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    align-content: center;
}
#submit-btn-group {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    justify-items: center;
    border-bottom: none;
}
#submit-btn {
    width: 50%;
    min-width: 4rem;
    height: 30px;
    padding: 0;
    margin: 1rem 0;
    overflow: hidden;
    border: 1px solid var(--font-dark);
    border-radius: 3px;
}
#submit-btn:hover {
    background: var(--grey-transparent);
}
#form-submit-success {
  width: 100%;
  color: var(--secondary-dark);
  margin: 0;
  padding: 0;
}
#form-success-head {
  margin: 0;
  padding: 0;
  margin-bottom: 1rem;
}
#form-success-body {
  margin: 0;
  padding: 0;
}
.form-error-node {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;
  align-content: center;
  border: 1px solid black;
}
#contact-selector-container {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  align-content: center;
  color: var(--secondary-dark);
}
.contact-selector {
  border: 1px solid black;
  width: 33%;
  border-radius: 3px;
  margin: 0rem;
  padding: 2px;
  margin-bottom: 0.25rem;
  display: flex;
  flex-direction: row;
  align-content: center;
  align-items: center;
  justify-content: center;
}
.contact-selector:hover {
  background: var(--secondary-dark-transparent);
  color: var(--primary);
  font-weight: bold;
}
.validatedInput {
  background: var(--secondary-dark-verytransparent);
}
.activeSelector {
  border: 2px solid black;
  background: var(--secondary-dark-transparent);
  color: var(--primary);
  font-weight: bold;
}
#contact-selector-main {
  width: 80%;
  color: var(--secondary-dark);
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  align-content: flex-start;
}
#contact-selector-main h3 {
  margin: 0;
  padding: 5px;
}
.contact-input-confirmed {
  color: var(--primary);
  font-weight: bold;
  margin: 0 0.5rem;
}
#contact-group-social-service {
  border-bottom: 0;
  margin-left: 2rem;
}
#contact-group-social-name {
  margin: 0;
  padding: 0 0 1rem 2rem;
}
#social-contact-form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: flex-start;
  align-items: flex-start;
  width: 100%;
}
#service-select{
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-content: flex-start;
  align-items: center;
  margin-top: 1rem;
}
#other-contact-input {
  border: 1px solid black;
  padding: 2px 5px;
}
.contactContainer {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  align-content: center;
  width: 100%;
}
.form-error-span {
  margin: 0 0.5rem;
  color: red;
  font-weight: bold;
}
#contact-selector-head {
  display: flex;
  flex-direction:row;
  justify-content: center;
  justify-items: center;
  align-content: center;
  align-items: center;
  width: 100%;
}
#contact-selector-head-detail {
  margin: 0;
  margin-bottom: 0.25rem;
}
.preferred-contact-type {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;
  align-content: center;
  align-self: center;
  width: 100%;
  padding: 0 5px;
  margin: 0;
  color: var(--font-dark);
}
@media screen and (max-width:400px) {
  #contact-selector-main {
    width: 100%;
  }
}
</style>
