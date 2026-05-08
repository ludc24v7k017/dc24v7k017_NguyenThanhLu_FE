<template>
    <div class="page">
        <h4>Thêm Liên hệ</h4>
        <ContactForm :contact="contact" @submit:contact="createContact" />
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
        async createContact(contact) {
            try {
                await ContactService.create(contact);
                alert('Liên hệ được thêm thành công.');
                // Chuyển về trang danh sách liên hệ
                this.$router.push({ name: "contactbook" });
            } catch (error) {
                console.log(error);
                alert("Lỗi: Không thể thêm liên hệ");
                // this.message = "Lỗi: Không thể thêm liên hệ";
            }
        },
    },
};
</script>