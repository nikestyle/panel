<script>
import IconGrid from '@/components/icons/IconGrid.vue'
import IconUser from '@/components/icons/IconUser.vue'
import IconHouse from '@/components/icons/IconHouse.vue'
import Authorization from '@/components/Authorization.vue'
import NavButton from './UI/navButton.vue'

export default {
   components: {
      IconGrid,
      IconUser,
      IconHouse,
      Authorization,
      NavButton
   },
   data() {
      return {
         dialogVisible: false,
         loginSuccess: false,
      }
   },
   methods: {
      showDialog() {
         this.dialogVisible = true
      },
      updateStatus() {
         this.dialogVisible = false
         this.loginSuccess = true
      },
      goToLogin() {
         setTimeout(() => {
            this.loginSuccess = false
         }, 500)
      }
   }
}
</script>

<template>
   <header
      class="d-flex flex-wrap align-items-center justify-content-center justify-content-md-between py-3 mb-4 border-bottom">
      <div class="col-md-3 mb-2 mb-md-0">
         <a href="/" class="d-inline-flex link-body-emphasis text-decoration-none">
            <svg class="bi" width="40" height="32" role="img" aria-label="Bootstrap">
               <use xlink:href="#bootstrap"></use>
            </svg>
         </a>
      </div>

      <ul class="nav col-12 col-md-auto mb-2 justify-content-center mb-md-0">
         <RouterLink to="/">
            <li><a href="#" class="nav-link btn-primary">
                  <IconHouse class="bi d-block mx-auto mb-1" />
                  Home
               </a>
            </li>
         </RouterLink>
         <RouterLink to="/products">
            <li><a href="#" class="nav-link btn-primary">
                  <IconGrid class="bi d-block mx-auto mb-1" />
                  Products
               </a>
            </li>
         </RouterLink>
         <RouterLink to="users">
            <li><a href="#" class="nav-link btn-primary">
                  <IconUser class="bi d-block mx-auto mb-1" />
                  Users
               </a>
            </li>
         </RouterLink>

      </ul>

      <div class="col-md-3 text-end">
         <Transition name="bounce">
            <navButton @click="showDialog" v-if="!loginSuccess">Login</navButton>
            <NavButton v-else @click="goToLogin" class="btn-danger">Exit</NavButton>
         </Transition>
      </div>
      <MyDialog v-model:show="dialogVisible">
         <template #modal-header>
            <h2>Authorization</h2>
         </template>
         <template #modal-body>
            <Authorization @authorization-success="updateStatus" />
         </template>
      </MyDialog>
   </header>
</template>
<style>
.bounce-enter-active {
   animation: bounce-in 0.5s;
}

.bounce-leave-active {
   animation: bounce-in 0.5s reverse;
}

@keyframes bounce-in {
   0% {
      transform: scale(0);
   }

   50% {
      transform: scale(1.25);
   }

   100% {
      transform: scale(1);
   }
}
</style>