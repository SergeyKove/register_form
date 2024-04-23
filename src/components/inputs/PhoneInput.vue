<template>
  <div class="text-field">
    <label class="text-field__label" for="phone">Номер телефона*</label>
    <input
      v-model="phone"
      id="phone"
      type="tel"
      class="text-field__input"
      :class="{ 'text-field__input_invalid': $v.phone.$error }"
      @blur="$v.phone.$touch()"
    />

    <span v-if="$v.phone.$error" class="text-field__message">
      <small v-if="!$v.phone.alpha"> Номер телефона должен начинаться с +7 </small>
      <small v-else> Поле обязательно для заполнения </small>
    </span>
  </div>
</template>

<script>
import { required } from 'vuelidate/lib/validators'

export default {
  props: {
    formData: {
      type: Object,
      default: () => ({})
    }
  },

  computed: {
    phone: {
      get() {
        return this.formData.phone
      },
      set(value) {
        this.$emit('onChange', { key: 'phone', value: value })
      }
    }
  },

  validations: {
    phone: {
      required,
      alpha: (val) => /^\+[\d]{11}$/i.test(val)
    }
  }
}
</script>
