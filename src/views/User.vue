<template>
    <div class="page">
        <h4>Đăng Nhập</h4>
        <userForm :user="user" @submit:user="signIn" />
        <p>{{ message }}</p>
    </div>
</template>
<script>
import userForm from "@/components/logInForm.vue";
import userService from "@/services/user.service";
export default {
    components: {
        userForm,
    },
    data() {
        return {
            user: {},
            message: "",
        };
    },
    methods: {
        async signIn(data) {
            console.log(data);
            try {
                this.user = await userService.get(this.user.email);
                if(data.email == this.user.email && data.password == this.user.password) {
                    this.$router.push({ name: "notes" });
                }
            } catch (error) {
                console.log(error);
            }
        },
    },
};
</script>
<style scoped>
    @import "@/assets/form.css";    
</style>