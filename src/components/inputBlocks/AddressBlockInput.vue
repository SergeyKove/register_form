<template>
  <div>
    <div class="text-field">
      <label class="text-field__label" for="index">Индекс</label>
      <input id="index" v-model="index" class="text-field__input" />
    </div>

    <div class="text-field">
      <label class="text-field__label" for="country">Страна</label>
      <input id="country" v-model="country" class="text-field__input" />
    </div>

    <div class="text-field">
      <label class="text-field__label" for="region">Область</label>
      <input id="region" v-model="region" class="text-field__input" />
    </div>

    <div class="text-field">
      <label class="text-field__label" for="city">Город*</label>
      <input
        id="city"
        v-model="city"
        class="text-field__input"
        @blur="$v.city.$touch()"
        :class="{ 'text-field__input_invalid': $v.city.$error }"
      />

      <span v-if="$v.city.$error" class="text-field__message">
        <small v-if="!$v.city.alpha"> Поле должно содержать только буквы </small>
        <small v-else> Поле обязательно для заполнения </small>
      </span>
    </div>

    <div class="text-field">
      <label class="text-field__label" for="street">Улица</label>
      <input id="street" v-model="street" class="text-field__input" />
    </div>

    <div class="text-field">
      <label class="text-field__label" for="house">Дом</label>
      <input id="house" v-model="house" class="text-field__input" />
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
    index: {
      get() {
        return this.formData.index
      },
      set(value) {
        this.$emit('onChange', { key: 'index', value: value })
      }
    },

    country: {
      get() {
        return this.formData.country
      },
      set(value) {
        this.$emit('onChange', { key: 'country', value: value })
      }
    },

    region: {
      get() {
        return this.formData.region
      },
      set(value) {
        this.$emit('onChange', { key: 'region', value: value })
      }
    },

    city: {
      get() {
        return this.formData.city
      },
      set(value) {
        this.$emit('onChange', { key: 'city', value: value })
      }
    },

    street: {
      get() {
        return this.formData.street
      },
      set(value) {
        this.$emit('onChange', { key: 'street', value: value })
      }
    },

    house: {
      get() {
        return this.formData.house
      },
      set(value) {
        this.$emit('onChange', { key: 'house', value: value })
      }
    }
  },

  validations: {
    city: {
      required,
      alpha: (val) => /^[а-яё]*$/i.test(val)
    }
  }
}
</script>
