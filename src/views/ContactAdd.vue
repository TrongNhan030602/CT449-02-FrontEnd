<template>
    <div
      v-if="contact"
      class="page"
    >
      <h4>Thêm Mới Liên hệ</h4>
      <ContactForm
        :contact="contact"
        @submit:contact="createContact"
      />
      <p>{{ message }}</p>
    </div>
  </template>
  
  <script>
  import ContactForm from "@/components/ContactForm.vue";
  import ContactService from "@/services/contact.service";
  export default {
    components: {
      ContactForm,
    },
    data() {
      return {
        contact: {},
        message: "",
      };
    },
    methods: {
      
      async createContact(data) {
        try {
          await ContactService.create(data);
          this.message = "Liên hệ được cập nhật thành công.";
        } catch (error) {
          console.log(error);
          this.$router.push({
            name: "notfound",
            params: {
              pathMatch: this.$route.path.split("/").slice(1),
            },
            query: this.$route.query,
            hash: this.$route.hash,
          });
        }
      },
     
    },
    created() {
      
      this.message = "";
    },
  };
  </script>
  