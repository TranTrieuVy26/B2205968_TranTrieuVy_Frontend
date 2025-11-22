<template>
  <div class="page">
    <h4>Thêm liên hệ</h4>
    <ContactForm
      :contact="contact"
      @submit:contact="addContact"
    />
    <p class="text-success">{{ message }}</p>
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
      contact: {
        name: "",
        email: "",
        address: "",
        phone: "",
        favorite: false,
      },
      message: "", 
    };
  },
  methods: {
    async addContact(data) {
      this.message = "Đang xử lý...";
      try {
       await ContactService.create(data);
        
        this.message = "Liên hệ đã được thêm mới thành công.";
        
       this.$router.push({ name: "contactbook" });
        
      } catch (error) {
        console.error("Lỗi khi thêm liên hệ:", error);
        this.message = "Đã xảy ra lỗi khi thêm liên hệ.";
      }
    },
  },
};
</script>

<style scoped>
.page {
  max-width: 600px;
  margin: 0 auto;
}
</style>