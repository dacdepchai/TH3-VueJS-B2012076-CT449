<template>
    <div v-if="contact" class="page">
     <h4>Thêm Liên hệ</h4>
        <ContactFormAdd
        :contact="contact" 
        @submit:contact="addContact"
        />
        <p>{{ message }}</p>
    </div>
</template>

<script>
    import ContactFormAdd from "../components/ContactFormAdd.vue";
    import ContactService from "@/services/contact.service";

    export default {
        components: {
            ContactFormAdd,
        },
       
        data() {
            return {
                contact:{},
                message: "",
            };
        },  
        methods: {
            async addContact(contact) {
                try {
                    await ContactService.create(contact);
                    this.message = "Liên hệ được cập nhật thành công.";
                } catch (error) {
                    console.log(error);
                }
            },

        },   
        created() {
            this.message = "";
        },
    };

</script>