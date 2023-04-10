<template>

  <div class="container my-3 " dir="rtl">
    <div class="row">
      <div class="col-md-4 border rounded p-4 mx-3">
        <Form class="" @submit="onSubmit">
          <label for="exampleInputText" class="form-label fs-6">نام و نام خانوادگی:</label>
          <Field class="form-control mb-2" id="exampleInputText" name="text" type="text" :rules="validateName"
                 :validateOnInput="true"/>
          <ErrorMessage class="fs-8 text-danger my-3" name="text"/>

          <label for="exampleInputEmail" class="form-label fs-6">ایمیل:</label>
          <Field class="form-control" id="exampleInputEmail" name="email" type="email" :rules="validateEmail"
                 :validateOnInput="true"/>
          <ErrorMessage class="fs-8 text-danger my-3" name="email"/>

          <label for="exampleInputPassword" class="form-label fs-6 mt-2">رمز عبور:</label>
          <Field class="form-control mb-2" id="exampleInputPassword" name="password" type="password"
                 :rules="validatePassword" :validateOnInput="true"/>
          <ErrorMessage class="fs-8 text-danger my-3" name="password"/>


          <button type="submit" class="btn btn-secondary mt-3">ثبت نام</button>

        </Form>


      </div>
    </div>
  </div>

</template>

<script>
import {Form, Field, ErrorMessage} from 'vee-validate';
import Swal from "sweetalert2";
import {inject} from "vue";


export default {
  name: "FormVeeValidation",
  components: {
    Form,
    Field,
    ErrorMessage
  },
  setup() {
    const message = inject('msg');

    function onSubmit(values) {
      console.log(values);

      Swal.fire({
        title: 'شما مجاز به ورود به پنل کاربری هستید',
        icon: 'success',
        showConfirmButton: false,
        timerProgressBar: true,
        timer: 3000,
        toast: true,
        position: 'top',
      });


    }

    function validateName(name) {
      if (!name) {
        return 'لطفا نام و نام خانوادگی خود را وارد نمایید!'
      }

      return true;
    }

    function validateEmail(email) {
      if (!email) {
        return 'لطفا رمز عبور خود را وارد نمایید!'
      }
      const regex = /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i;
      if (!regex.test(email)) {
        return 'لطفا ایمیل خود را بصورت صحیح وارد نمایید!';
      }

      return true;
    }

    function validatePassword(password) {
      if (!password) {
        return 'لطفا رمز عبور خود را وارد نمایید!'
      }

      // const regex = /^(?=.*[A-Za-z])(?=.*\d)[A-Za-z\d]{8,}$/;

      if (password.length < 6) {
        return 'رمز عبور وارده کمتر از 6 رقم می باشد!'
      }

      return true;
    }

    return {onSubmit, validateEmail, validateName, validatePassword, message}
  }
}
</script>

<style scoped>
.fs-8 {
  font-size: 0.8rem;
  display: block;
}
</style>