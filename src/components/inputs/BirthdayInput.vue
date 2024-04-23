<template>
  <div class="text-field">
    <label class="text-field__label" for="birthday">Дата рождения*</label>
    <input
      id="birthday"
      type="date"
      v-model="birthday"
      @blur="$v.birthday.$touch()"
      class="text-field__input"
      :class="{ 'text-field__input_invalid': $v.birthday.$error }"
    />

    <span v-if="$v.birthday.$error" class="text-field__message">
      <small> Поле обязательно для заполнения </small>
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
    birthday: {
      get() {
        return this.formData.birthday
      },
      set(value) {
        this.$emit('onChange', { key: 'birthday', value: value })
      }
    }
  },

  validations: {
    birthday: {
      required
    }
  }
}
</script>
