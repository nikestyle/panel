<script>
export default {
   data() {
      return {
         email: '',
         password: '',
         alertActive: false,
         alertMessage: '',
         alertColor: false,
         dataSuccess: false
      }
   },
   methods: {
      login: function () {
         this.alertMessage = ''

         if (this.email === 'max@email.com') {
            if (this.password.length >= 6) {
               this.alertActive = false;
               this.dataSuccess = true;
               this.alertColor = true;
               setTimeout(() => {
                  this.alertActive = true
                  this.dataSuccess = false;
                  this.alertMessage = 'Success';
               }, 1000)
               setTimeout(() => {
                  this.$emit('authorization-success');
                  this.$emit('login-success');
               }, 2000)
            } else {
               this.alertActive = true
               this.alertMessage = 'The password must contain at least 6 characters';
               this.alertColor = false;
            }
         } else {
            this.alertActive = true
            this.alertMessage = 'Email is not correct';
            this.alertColor = false;
         }
      },
   }
}
</script>
<template>
   <div class="container">
      <div class="row justify-content-center">
         <div class="col-md-12">
            <div class="card">
               <div class="card-body">
                  <form @submit.prevent="login">
                     <div class="form-group">
                        <label for="email">Email:</label>
                        <input type="email" class="form-control" id="email" v-model="email" required>
                     </div>
                     <div class="form-group mb-2">
                        <label for="password">Password:</label>
                        <input type="password" class="form-control" id="password" v-model="password" required>
                     </div>
                     <button type="submit" class="btn btn-primary"><span v-if="!dataSuccess">Join</span>
                        <div v-else class="spinner-border" role="status">

                        </div>
                     </button>
                  </form>
               </div>
            </div>
         </div>
      </div>

      <div v-if="alertActive" class="row justify-content-center mt-3">
         <div class="col-md-6">
            <div class="alert" :class="{ 'alert-success': alertColor, 'alert-danger': !alertColor }" role="alert">
               {{ alertMessage }}
            </div>
         </div>
      </div>
   </div>
</template>