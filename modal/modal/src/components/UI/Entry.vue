<template>
    <modal title="Entry" @close="$emit('closer').clos()">
        <div slot="body">
            <form >
              <label>Email:</label>
              <input type="email" required v-model="data.email">
              <label>Password:</label>
              <input type="text" required v-model="data.password">
              <button class="btn btnPrimary" @click="getDatas">Submit!</button>
              <button class="btn btnDanger" @click="$emit('closerr')">Registration</button>
              
              
            </form>
        </div>

          
          
    </modal>
</template>

<script>
import modal from '@/components/UI/Modal.vue'


export default {
    components: { modal },
    data(){
        return{
            data:{
                email: '',
                password: ''
            }
        }
    },
    methods:{
        getDatas () {
      console.log({
        name: this.data.email,
        email: this.data.password
      })
      this.data.email = ''
      this.data.password = ''
      

    },
    // обновляем  поля при зкрытиии 
    clos(){
        this.data.email = ''
        this.data.password = ''
      }
    }
    
    
}


</script>