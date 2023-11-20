<template>
  <div @click.self="close" v-if="isOpen" class="popup">
    <div class="popup__wrapper">
      <button @click="$emit('close')" class="popup__close" type="button">X</button>
      <div class="popup__title">Header</div>
      <div class="popup__content">
        <slot></slot>
      </div>
      <div class="popup__footer">
        <button @click="close" class="popup__btn">Cancel</button>
        <button @click="confirmed" class="popup__btn">Ok</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    isOpen: {
      type: Boolean,
      required: true,
    },
  },
  emits: {
    ok: null,
    close: null,
  },
  mounted() {
    document.addEventListener("keydown", this.handlerKeyDown);
  },
  beforeUnmount() {
    document.addEventListener("keydown", this.handlerKeyDown);
  },
  methods: {
    close() {
      this.$emit('close');
    },
    confirmed() {
      this.$emit('ok');
    },
    handlerKeyDown(e) {
      if(this.isOpen && e.key === 'Escape') {
        this.close();
      }
    },
  },
}
</script>

<style>
  .popup {
    position: fixed;
    inset: 0;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .popup__wrapper {
    width: 500px;
    padding: 40px 20px 20px;
    background-color: #ffffff;
    color: #000000;
    text-align: center;
    position: relative;
  }
  .popup__close {
    position: absolute;
    right: 10px;
    top: 10px;
    padding: 5px;
  }
  .popup__content {
    margin-top: 30px;
  }
  .popup__footer {
    border-top: 1px solid #000000;
    margin-top: 30px;
    padding-top: 30px;
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
  }
  .popup__btn {
    display: flex;
    justify-content: center;
    padding: 10px 20px;
    right: 5px;
    background-color: blue;
    color: #ffffff;
    min-width: 100px;
    border: none;
  }
</style>
