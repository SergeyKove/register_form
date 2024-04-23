<template>
  <div>
    <div class="text-field">
      <label class="text-field__label" for="lastName">Фамилия*</label>
      <input
        v-model="lastName"
        id="lastName"
        type="text"
        class="text-field__input"
        :class="{ 'text-field__input_invalid': $v.lastName.$error }"
        @blur="$v.lastName.$touch()"
      />

      <div v-if="$v.lastName.$error" class="text-field__message">
        <small v-if="!$v.lastName.alpha"> Поле должно содержать только буквы </small>
        <small v-else> Поле обязательно для заполнения </small>
      </div>
    </div>

    <div class="text-field">
      <label class="text-field__label" for="lastName">Имя*</label>
      <input
        type="text"
        class="text-field__input"
        v-model="name"
        @blur="$v.name.$touch()"
        :class="{ 'text-field__input_invalid': $v.name.$error }"
      />

      <span v-if="$v.name.$error" class="text-field__message">
        <small v-if="!$v.name.alpha"> Поле должно содержать только буквы </small>
        <small v-else> Поле обязательно для заполнения </small>
      </span>
    </div>

    <div class="text-field">
      <label class="text-field__label" for="lastName">Отчество</label>
      <input type="text" class="text-field__input" v-model="middleName" />
    </div>
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
    lastName: {
      get() {
        return this.formData.lastName
      },
      set(value) {
        this.$emit('onChange', { key: 'lastName', value: value })
      }
    },

    name: {
      get() {
        return this.formData.name
      },
      set(value) {
        this.$emit('onChange', { key: 'name', value: value })
      }
    },

    middleName: {
      get() {
        return this.formData.middleName
      },
      set(value) {
        this.$emit('onChange', { key: 'middleName', value: value })
      }
    }
  },

  validations: {
    lastName: {
      required,
      alpha: (val) => /^[а-яё]*$/i.test(val)
    },

    name: {
      required,
      alpha: (val) => /^[а-яё]*$/i.test(val)
    }
  }
}
</script>
