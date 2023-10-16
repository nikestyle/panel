<template>
   <div v-if="show" @click="hideDialog" class="modal" tabindex="-1" role="dialog">
      <div class="modal-dialog" role="document">
         <div @click.stop class="modal-content">
            <div class="modal-header text-black">
               <slot name="modal-header"></slot>
               <button @click="hideDialog" type="button" class="btn-close" aria-label="Close">
               </button>
            </div>
            <div class="modal-body">
               <slot name="modal-body"></slot>
            </div>
         </div>
      </div>
   </div>
</template>

<script>
export default {
   name: 'MyDialog',
   props: {
      show: {
         type: Boolean,
         default: false
      }
   },
   data() {
      return {

      }
   },
   methods: {
      hideDialog() {
         this.$emit('update:show', false)
      },
   },
   computed: {

   },
}
</script>

<style lang="scss" scoped>
.modal {
   display: block;
}
</style>