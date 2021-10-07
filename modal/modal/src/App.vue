<template>
  <div class="wrapper">
    <div class="wrapper-content">

      <section>
        <div class="container">

          <!-- first modal -->
          <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Show first modal</button>
          <modals
            title="First modal"
            v-show="modalFirst"
            @close="modalFirst = false">
            <!-- body -->
            <div slot="body">
              <p> Text Text Text Text Text Text Text </p>
              <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Well Done!</button>
            </div>
          </modals>

          <!-- second modal -->
          <button class="btn btnPrimary" @click="modalSecond.show = !modalSecond.show">Show modal with form</button>
          <modals
            title="Modal with form"
            v-show="modalSecond.show"
            @close="modalSecond.show = false">
            <!-- body -->
            <div slot="body">
              <form @submit.prevent="submitSecondForm">
                <label>Name:</label>
                <input type="text" required v-model="modalSecond.name">
                <label>Email:</label>
                <input type="email" required v-model="modalSecond.email">
                <button class="btn btnPrimary">Submit!</button>
              </form>
            </div>
          </modals>

          <!-- modal with validate -->
          <button class="btn btnPrimary" @click="modalValidate = !modalValidate">Show modal with form + validate</button>
          <modalValidate v-show="modalValidate" @close="modalValidate = false"/>
          


          <!--Entry-->
          <button class="btn btnPrimary" @click="entry = !entry">Вход на сайт</button>
          <entry v-show="entry" @closer="entry = false" @closerr="enter()"/>

          <!--Registration-->
          <button class="btn btnPrimary" @click="registration = !registration">Зарегестрироваться</button>
          <registration v-show="registration" @closer="registration = false" @open="openn()"/>
        </div>
      </section>


    </div>
  </div>
</template>

<script>
import modals from '@/components/UI/Modal.vue'
import modalValidate from '@/components/ModalValidate.vue'
import entry from '@/components/UI/Entry.vue'
import registration from '@/components/UI/Registration.vue'

export default {
  components: { modals, modalValidate, entry, registration },
  data () {
    return {
      modalFirst: false,
      modalSecond: {
        show: false,
        name: '',
        email: ''
      },
      modalValidate: false,
      entry: false,
      registration: false
    }
  },
  methods: {
    submitSecondForm () {
      console.log({
        name: this.modalSecond.name,
        email: this.modalSecond.email
      })
      this.modalSecond.name = ''
      this.modalSecond.email = ''
      this.modalSecond.show = false

    },
    enter(){
      this.registration = true,
      this.entry = false
    },
    openn(){
      this.entry = true,
      this.registration = false
    }
  }
}
</script>
