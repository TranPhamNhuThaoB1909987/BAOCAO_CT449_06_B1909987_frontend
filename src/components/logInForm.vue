<template>
    <Form @submit="SignIn" :validation-schema="dangnhap_form">
        <div class="form-group">
            <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcShmghVaF4Wa87EiJ30rqhwx81O6O5kYTc2P6gqVfGKzJ3rEy_TxIs6W5WCcdiJk3IIfhc&usqp=CAU ">
            <label for="email">E-mail</label>
            <Field name="email" type="email" class="form-control" v-model="userLocal.email" />
            <ErrorMessage name="email" class="error-feedback" />
        </div>
        <div class="form-group">
            <label for="password">Mật Khẩu</label>
            <Field name="password" type="password" class="form-control" v-model="userLocal.password" />
            <ErrorMessage name="password" class="error-feedback" />
        </div>
        <div class="form-group">
            <button class="btn btn-primary">Đăng Nhập</button>
            <button type="button" class="ml-2 btn btn-danger" @click="gotoSignUp">
                Đăng Ký
            </button>
        </div>
    </Form>
</template>
<script>
import * as yup from "yup";
import { Form, Field, ErrorMessage } from "vee-validate";
export default {
    components: {
        Form,
        Field,
        ErrorMessage,
    },
    emits: ["submit:user"],
    props: {
        user: { type: Object, required: true }
    },
    data() {
        const dangnhap_form = yup.object({
            email:yup
                .string().required("Email không được để trống !")
                .email("Email không chính xác !")
                .max(50,"Email tối đa 50 ký tự !"),
            password:yup
                .string()
                .required("Mật khẩu không được để trống !")
                .min(4,"Mật khẩu tối thiểu 4 ký tự !")
        })
        return {
            userLocal: this.user,
            dangnhap_form,
        };
    },
    methods: {
        SignIn() {
            console.log(this.userLocal);
            this.$emit("submit:user", this.userLocal);
        },
        gotoSignUp(){
            this.$router.push({ name: "register" });
        }
    },
};
</script>
<style scoped>
    @import "@/assets/form.css";
    @import "@/assets/main.css";
</style>