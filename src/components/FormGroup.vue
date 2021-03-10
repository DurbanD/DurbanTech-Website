<template>
  <div class="contact-group">
    <label v-if="label" class="form-label-container">
      <p class="form-label"><span v-if="errorStatus" class="form-error-span">*</span>{{ label }} </p>
      <p v-if="errorStatus" class="form-error">{{ errorMessage }}</p>
    </label>

    <input
    v-if="!isTextArea && !isOptionSelect"
    class="form-input"
    :type="type"
    :placeholder="placeholder"
    :value="value"
    @input="$emit('input', $event.target.value)" >

    <div id="form-option-container" v-if="isOptionSelect">
      <select v-if="isOptionSelect" id="form-select" :value="value" @change="$emit('input', $event.target.value)">
        <option value="" selected>{{ optionSelectText }}</option>
        <option v-for="opt in optionList" id="form-select-options" :key="opt.value" :value="opt.value">{{ opt.name }}</option>
      </select>
      <p v-if="errorStatus" class="form-error">{{ errorMessage }}</p>
    </div>

    <textarea
    v-if="isTextArea"
    id="form-message"
    :value="value"
    :type="type"
    :placeholder="placeholder"
    @input="$emit('input', $event.target.value)" />
  </div>
</template>

<script>
import { Vue } from 'vue-property-decorator'

const FormGroup = Vue.extend({
  data () {
    return {
      optionSelectText: 'Choose Service'
    }
  },
  props: {
    label: String,
    type: String,
    placeholder: String,
    value: {
      type: String,
      required: true
    },
    errorStatus: Boolean,
    errorMessage: String,
    optionList: Array
  },
  components: {
    // ContactSocialSelect
  },
  computed: {
    isTextArea () {
      return this.type === 'textarea'
    },
    isOptionSelect () {
      return this.type === 'opt'
    }
  }
})
export default FormGroup
</script>

<style scoped>
.contact-group {
    padding: 1rem 2rem;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    justify-content: space-between;
    align-items: flex-start;
    border-bottom: 1px solid black;
    border-radius: 1px;
}
.form-label {
    color: var(--font-dark);
    display: flex;
    justify-content: center;
    align-content: center;
    align-items: center;
    padding: 0.5rem;
    margin: 0;
    font-weight: bold;
}
.form-input,
textarea {
    width: 90%;
    border: 1px solid black;
    margin: 1rem 0 0 1rem;
    border-radius: 3px;
    padding: 2px 5px;
}
#form-select {
  border: 0;
  width: 30%;
  min-width: 100px;
  padding: 1px 5px;
  margin: 0;
  margin-left: 1rem 0 0 1rem;
}
#form-select-options {
  padding: 1px 5px;
  margin: 0;
}
#form-message {
    width: 95%;
    height: 100px;
    max-height: 25vh;
    resize: vertical;
    overflow: auto;
    padding: 8px;
}
.form-label-container,
#form-option-container {
  width: 100%;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  justify-items: space-between;
}
.form-error {
  border: 1px solid black;
  border-radius: 5px;
  padding: 3px 10px;
  color: red;
}
.form-error-span {
  margin: 0 0.5rem;
  color: red;
}
@media screen and (max-width:500px) {
  .contact-group {
    padding: 0.5rem 1rem;
  }
  .form-input,
  textarea {
    margin: 0.5rem;
    width: 100%;
  }
}
</style>
