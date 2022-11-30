<template>
    <Form @submit="SignUp" :validation-schema="dangky_form">
        <div class="form-group">
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
            <label for="confirmPassword">Xác Nhận Lại Mật Khẩu</label>
            <Field name="confirmPassword" type="password" class="form-control" v-model="userLocal.confirmPassword" />
            <ErrorMessage name="confirmPassword" class="error-feedback" />
        </div>
        <div class="form-group">
            <button class="btn btn-primary">Đăng Ký</button>
            <button type="button" class="ml-2 btn btn-danger" @click="gotoSignIn">
                Đăng Nhập
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
        const dangky_form = yup.object({
            email:yup
                .string().required("Email không được để trống !")
                .email("Email không chính xác !")
                .max(50,"Email có tối đa 50 ký tự !"),
            password:yup
                .string()
                .required("Mật khẩu không được để trống !")
                .min(4,"Mật khẩu tối thiểu 4 ký tự !"),
            confirmPassword:yup
                .string()
                .required("Mật khẩu không được để trống !")
                .min(4,"Mật khẩu tối thiểu 4 ký tự !")
        })
        return {
            userLocal: this.user,
            dangky_form,
        };
    },
    methods: {
        SignUp() {
            console.log(this.userLocal);
            this.$emit("submit:user", this.userLocal);
        },
        gotoSignIn(){
            this.$router.push({ name: "user" });    
        }
    },
};
</script>
<style scoped>
@import "@/assets/form.css";
</style>