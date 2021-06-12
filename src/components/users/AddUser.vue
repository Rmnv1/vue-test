<template>
  <div>
    <button class="btn btn--center btn--modal" @click="toggleModal">
      Добавить пользователя
    </button>
    <transition name="fade">
      <modal
        modalTitle="Добавить пользователя"
        v-if="modalIsVisible"
        @toggleModal="toggleModal"
      >
        <form action="/" class="modal-form" @submit.prevent="addUser">
          <label for="name" class="modal-form__label">
            Имя
            <input
              type="text"
              id="name"
              name="name"
              class="modal-form__field"
              placeholder="Введите имя *"
              required
              v-model="name"
            />
          </label>
          <label for="phone" class="modal-form__label">
            Телефон
            <input
              type="number"
              id="phone"
              name="phone"
              class="modal-form__field"
              placeholder="Введите телефон *"
              required
              v-model="phone"
              @input="limitPhoneLength"
            />
          </label>
          <label for="chief" class="modal-form__label">
            Начальник
            <select
              name="chief"
              id="chief"
              class="modal-form__list"
              v-model="chief"
            >
              <option selected disabled value="">Выберите начальника</option>

              <option v-for="chief in listOfChiefs" :key="chief.id">
                {{ chief }}
              </option>
            </select>
          </label>
          <button class="btn btn--modal btn--center">Добавить</button>
        </form>
      </modal>
    </transition>
  </div>
</template>

<script>
import Modal from "@/components/modal/Modal.vue";

export default {
  data() {
    return {
      // Users data
      name: "",
      phone: "",
      chief: "",

      // Наверное, не лучшее и не универсальное решение, но маски и полноценные валидации будут только в нечитаемых регулярках, которые займут кучу места, вряд ли это нужно для тестового задания, где не требовалась валидация :)
      phoneMaxLength: 11,

      // Modal state
      modalIsVisible: false,
    };
  },
  props: ["addNewUser", "listOfChiefs"],
  components: {
    Modal,
  },
  methods: {
    toggleModal() {
      this.modalIsVisible = !this.modalIsVisible;
    },

    addUser() {
      this.addNewUser({
        name: this.name,
        phone: this.phone,
        chief: this.chief,
        staff: [],
      });

      // Clear inputs
      this.name = "";
      this.phone = "";
      this.chief = "";

      // Close modal
      this.toggleModal();
    },

    limitPhoneLength() {
      const maxLength = 11;
      if (this.phone.length > maxLength) this.phone = this.phone.substr(0, maxLength);
    },
  },
};
</script>
