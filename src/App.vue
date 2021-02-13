<template>
  <div id="app">
    <div class="grid">
      <contact-card
        v-for="item in contacts"
        :key="item.id"
        :contact="item"
        @edit="editContact"
        @remove="removeContact"
      />
      <div class="add-contact" @click="addContact"></div>
    </div>
    <sidebar v-model:visible="visibleLeft" class="p-sidebar-md" position="left">
      <contact-form
        :contact-data="selectedContact"
        @save="saveContact"
      />
    </sidebar>
  </div>
</template>

<script>

import contactCard from '@/components/contact-card'
import contactForm from '@/components/contact-form'
import sidebar from 'primevue/sidebar'

import contactData from '@/data.js'

export default {
  name: 'App',

  components: {
    contactCard,
    contactForm,
    sidebar
  },

  data() {
    return {
      contacts: [...contactData],
      visibleLeft: false,
      selectedContact: {}
    }
  },

  methods: {
    addContact() {
      this.selectedContact = {}
      this.visibleLeft = true
    },

    editContact(contactData) {
      this.selectedContact = {...contactData}
      this.visibleLeft = true
    },

    removeContact(id) {
      this.contacts = this.contacts.filter(el => el.id !== id)
    },

    saveContact(contactData) {
      let contactIndex = this.contacts.findIndex(item => item.id === contactData.id)

      if (contactIndex !== -1) {
        this.contacts[contactIndex] = contactData
      } else {
        this.contacts.push(contactData)
      }

      this.visibleLeft = false
    }
  }
};
</script>

<style lang="scss" scoped>

.grid {
  display: flex;
  flex-wrap: wrap;
  padding: .5rem;
}

.add-contact {
  @extend .base-card;

  background: #e8e8e8;
  border: none;
  cursor: pointer;

  &:after {
    content: '+';
    font: 2.5rem arial;
    color: #c0c0c0;
    border: 3px solid #c0c0c0;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 3rem;
    height: 3rem;
    @extend .center-center;
  }

  &:hover:after {
    color: #090;
    border-color: #090;
  }
}

@media screen and (max-width: 1080px) {
  .grid  {
    flex-direction: column;

    .contact {
      width: auto;
    }
  }
}
</style>
