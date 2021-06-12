<template>
  <div class="modal-wrap">

    <div class="overlay" @click="toggleModal"></div>

    <div class="modal">
      <div class="modal__header">
        <span class="modal__title">{{modalTitle}}</span>
        <button class="modal__close" @click="toggleModal">&times;</button>
      </div>
      <div class="modal__body">
        <slot></slot>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  props: {
    modalTitle: {
      type: String,
      required: true
    },
  },
  methods: {
    toggleModal() {
      this.$emit('toggleModal');
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
  .overlay{
    position: fixed;
    z-index: 10;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: table;
    transition: opacity 0.3s ease;
  }
  .modal{
    width: 100%;
    max-width: 450px;
    border-radius: 6px;
    background-color: #FFF;
    overflow: hidden;
    z-index: 11;
    position: fixed;
    transform: translate(-50%, -50%);
    top: 50%;
    left: 50%;
  }
  .modal__header{
    margin-bottom: 15px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #DDECFF;
    padding: 20px;
  }
  .modal__title{
    font-weight: 600;
  }
  .modal__close{
    border: none;
    background-color: transparent;
    font-size: 22px;
    cursor: pointer;
  }
  .modal__body{
    padding: 20px;
  }
  .modal-form {
    width: 100%;
    max-width: 450px;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
  }
  .modal-form__label{
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 10px 0px;
    font-size: 14px;
    &:first-child{
      margin-top: 0;
    }
  }
  .modal-form__field{
    width: 100%;
    max-width: 200px;
    padding: 8px;
    border: none;
    border-bottom: 1px solid #e0e0e0;
    padding-left: 12px;
    font-size: 14px;
  }
  .modal-form__list{
    width: 100%;
    max-width: 200px;
    padding: 8px;
    border: none;
    border-bottom: 1px solid #e0e0e0;
  }
  // Vue default styles
  .fade-enter-active, .fade-leave-active {
    transition: opacity .3s;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }
</style>