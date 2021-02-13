<template>
  <h2 v-if="formData.id">Editcontact</h2>
  <h2 v-else>Add new contact</h2>
  <form class="form">
    <div class="p-fluid">
      <div class="p-field">
        <label for="inputtext">Name</label>
        <InputText id="inputtext" type="text" v-model="formData.name" />
      </div>

      <div class="p-field">
        <label for="inputtext">Role</label>
        <InputText id="inputtext" type="text" v-model="formData.role" />
      </div>

      <div class="p-field">
        <label for="inputtext">Company</label>
        <InputText id="inputtext" type="text" v-model="formData.company" />
      </div>

      <div class="p-field">
        <label for="inputtext">Street</label>
        <InputText id="inputtext" type="text" v-model="formData.street" />
      </div>

      <div class="p-field suite">
        <label for="inputtext">Suite</label>
        <InputText id="inputtext" type="text" v-model="formData.suite" />
      </div>

      <div class="p-field city">
        <label for="inputtext">City</label>
        <InputText id="inputtext" type="text" v-model="formData.city" />
      </div>

      <div class="p-field state">
        <label for="inputtext">State</label>
        <InputText id="inputtext" type="text" v-model="formData.state" />
      </div>

      <div class="p-field zip">
        <label for="inputtext">Zip</label>
        <InputMask mask="99999" v-model="formData.zip" placeholder="99999" />
      </div>

      <div class="p-field">
        <label for="inputtext">Phone</label>
        <InputMask mask="(999) 999-9999" v-model="formData.phone" placeholder="(999) 999-9999" />
      </div>
    </div>
    <div class="form-footer">
      <Button label="Save" class="btn-submit p-button-raised" @click="save"/>
    </div>
  </form>
</template>

<script>
import InputText from 'primevue/inputtext'
import InputMask from 'primevue/inputmask'
import Button from 'primevue/button'

export default {
  name: 'contact-form',

  components: {
    InputText,
    InputMask,
    Button
  },

  props: {
    contactData: {
      type: Object,
      default: () => ({})
    }
  },

  emits: ['save'],

  data() {
    return {
      formData: {}
    }
  },

  created() {
    this.formData = this.contactData
  },

  methods: {
    save() {
      if (!this.formData.id) {
        this.formData.id = Date.now().toString(26)
      }
      this.$emit('save', this.formData)
    }
  }
}
</script>

<style lang="scss" scoped>

h2 {
  font-size: 1.5rem;
  padding: 1rem 0;
}

.form {
  .p-field {
    margin-bottom: .5rem;

    label {
      color: #08e;
      line-height: 1.5;
    }

    .p-inputtext {
      color: #000;

      &::placeholder {
        color: #a8a8a8;
      }
    }

    &.city {
      @extend .inline;
      width: 60%;
      margin-right: 5%;
    }

    &.state {
      @extend .inline;
      width: 10%;
      margin-right: 5%;
    }

    &.zip {
      @extend .inline;
      width: 20%;
    }
  }

  &-footer {
    text-align: center;

    .btn-submit {
      width: 96px;
      margin: .5rem auto;
    }
  }
}

</style>