<template>
  <div class="text-field">
    <label class="text-field__label" for="city">Лечащий врач</label>
    <select v-model="doctors" class="text-field__input">
      <option>Иванов</option>
      <option>Захаров</option>
      <option>Чернышева</option>
    </select>
  </div>
</template>

<script>
export default {
  props: {
    formData: {
      type: Object,
      default: () => ({})
    }
  },

  computed: {
    doctors: {
      get() {
        return this.formData.doctors
      },
      set(value) {
        this.$emit('onChange', { key: 'doctors', value: value })
      }
    }
  }
}
</script>
