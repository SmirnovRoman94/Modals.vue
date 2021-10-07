<template>
    <modal
      title="Registration"
      @close="$emit('closer').clos()">
      <!-- body -->
      <div slot="body">
        <form>
  
          <!-- name -->
          <div class="form-item" :class="{ errorInput: $v.name.$error }">
            <label>Name:</label>
            <p class="errorText" v-if="!$v.name.required"> Filed is required! </p>
            <p class="errorText" v-if="!$v.name.minLength"> Name must have at least {{ $v.name.$params.minLength.min }} !</p>
            <input
              v-model="name"
              :class="{ error: $v.name.$error }"
              @change="$v.name.$touch()">
          </div>
          
          <!-- lastname -->
          <div class="form-item" :class="{ errorInput: $v.lastname.$error }">
            <label>lastname:</label>
            <p class="errorText" v-if="!$v.lastname.required"> Filed is required! </p>
            <p class="errorText" v-if="!$v.lastname.minLength"> Name must have at least {{ $v.lastname.$params.minLength.min }} !</p>
            <input
              v-model="lastname"
              :class="{ error: $v.lastname.$error }"
              @change="$v.lastname.$touch()">
          </div>

          <!-- birthday -->
          <div class="form-item" :class="{ errorInput: $v.birthday.$error }">
            <label>birthday:</label>
            <p class="errorText" v-if="!$v.birthday.required"> Filed is required! </p>
            <input
                type="date"
              v-model="birthday"
              :class="{ error: $v.birthday.$error }"
              @change="$v.birthday.$touch()">
          </div>

          <!-- email -->
          <div class="form-item" :class="{ errorInput: $v.email.$error }">
            <label>Email:</label>
            <p class="errorText" v-if="!$v.email.required"> Filed is required! </p>
            <p class="errorText" v-if="!$v.email.email"> Email is not correct!</p>
            <input
              v-model="email"
              :class="{ error: $v.email.$error }"
              @change="$v.email.$touch()">
          </div>
  
  
          <!--password-->
          <div class="form-item" :class="{errorInput: $v.password.$error}">
            <label>Password</label>
              <p class="errorText" v-if="!$v.password.required">Password is required.</p>
              <p class="errorText" v-if="!$v.password.minLength">Password must have at least {{ $v.password.$params.minLength.min }} letters.</p>
              <input v-model.trim="password" 
                      :class="{error: $v.password.$error}"
                      @change="$v.password.$touch()"/>
          </div>
          <div class="form-item" :class="{ errorInput: $v.repeatPassword.$error }">
              <label>Repeat password</label>
                <p class="errorText" v-if="!$v.repeatPassword.sameAsPassword">Passwords must be identical.</p>
                <input :class="{error: $v.repeatPassword.$error}"
                        v-model.trim="$v.repeatPassword.$model"
                        />
          </div>
          <!-- button -->
          <button class="btn btnPrimary"  @click.prevent="getDatas">Submit!</button>
          <button class="btn btnDanger" @click.prevent="$emit('open')">Вход</button>
        </form>
      </div>
    </modal>
  </template>
  
  <script>
  import { required, minLength, email, sameAs } from 'vuelidate/lib/validators'
  
  import modal from '@/components/UI/Modal.vue'
  
  export default {
    components: { modal },
    data () {
      return {
        name: '',
        lastname: '',
        birthday: Date,
        email: '',
        password: '',
        repeatPassword: ''
      }
    },
    validations: {
      name: {
        required,
        minLength: minLength(4)
      },
      lastname: {
        required,
        minLength: minLength(6)
      },
      birthday:{
        required
      },
      email: {
        required,
        email
      },
      password: {
        required,
        minLength: minLength(6)
      },
      repeatPassword: {
        sameAsPassword: sameAs('password')
      }
    },
    methods: {
        getDatas () {
        this.$v.$touch()
        if (!this.$v.$invalid) {
          const user = {
            name: this.name,
            birthday: this.birthday,
            lastname: this.lastname,
            email: this.email,
            password: this.password
          }
          console.log(user)
  
          // DONE!
          this.name = ''
          this.birthday = Date,
          this.lastname= ''
          this.email = ''
          this.password = ''
          this.repeatPassword = ''
          this.$v.$reset()
          this.$emit('close')
        }
      },
      // обновляем  поля при зкрытиии 
      clos(){
        this.name = ''
        this.birthday =  Date,
        this.lastname = ''
        this.email = ''
        this.password = ''
        this.repeatPassword = ''
        this.$v.$reset()
      }
  
    }
  }
  </script>
  
  <style lang="scss">
  .form-item .errorText {
    display: none;
    margin-bottom: 8px;
    font-size: 13.4px;
    color: #de4040;
  }
  .form-item {
    &.errorInput .errorText {
      display: block;
    }
  }
  input.error {
    border-color: #de4040;
  }
  
  </style>
  