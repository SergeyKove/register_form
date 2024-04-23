<template>
  <div class="text-field">
    <label class="text-field__label" for="birthday">Пол</label>

    <div class="radio-box">
      <div class="radio">
        <label class="custom-radio">
          <input type="radio" value="Мужской" name="gender" v-model="gender" />
          <span>Мужской</span>
        </label>
      </div>

      <div class="radio">
        <label class="custom-radio">
          <input type="radio" value="Женский" name="gender" v-model="gender" />
          <span>Женский</span>
        </label>
      </div>
    </div>
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
    gender: {
      get() {
        return this.formData.gender
      },
      set(value) {
        this.$emit('onChange', { key: 'gender', value: value })
      }
    }
  }
}
</script>

<style scoped>
.radio-box {
  display: flex;
}

.radio-box :first-child {
  margin-right: 20px;
}
</style>
