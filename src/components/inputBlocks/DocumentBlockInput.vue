<template>
  <div>
    <div class="text-field">
      <label class="text-field__label" for="city">Тип документа*</label>
      <select
        v-model="documentType"
        class="text-field__input"
        :class="{ 'text-field__input_invalid': $v.documentType.$error }"
        @blur="$v.documentType.$touch()"
      >
        <option>Паспорт</option>
        <option>Свидетельство о рождении</option>
        <option>Водительское удостоверение</option>
      </select>

      <span v-if="$v.documentType.$error" class="text-field__message">
        <small> Поле обязательно для заполнения </small>
      </span>
    </div>

    <div class="text-field">
      <label class="text-field__label" for="documentSeries">Серия</label>
      <input id="documentSeries" type="text" v-model="documentSeries" class="text-field__input" />
    </div>

    <div class="text-field">
      <label class="text-field__label" for="documentNumber">Номер</label>
      <input id="documentNumber" type="text" v-model="documentNumber" class="text-field__input" />
    </div>

    <div class="text-field">
      <label class="text-field__label" for="documentDepartment">Кем выдан</label>
      <input
        id="documentDepartment"
        type="text"
        v-model="documentDepartment"
        class="text-field__input"
      />
    </div>

    <div class="text-field">
      <label class="text-field__label" for="documentCreate">Дата выдачи*</label>
      <input
        id="documentCreate"
        type="date"
        v-model="documentCreate"
        class="text-field__input"
        :class="{ 'text-field__input_invalid': $v.documentCreate.$error }"
        @blur="$v.documentCreate.$touch()"
      />

      <span v-if="$v.documentCreate.$error" class="text-field__message">
        <small> Поле обязательно для заполнения </small>
      </span>
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
    documentType: {
      get() {
        return this.formData.documentType
      },
      set(value) {
        this.$emit('onChange', { key: 'documentType', value: value })
      }
    },

    documentSeries: {
      get() {
        return this.formData.documentSeries
      },
      set(value) {
        this.$emit('onChange', { key: 'documentSeries', value: value })
      }
    },

    documentNumber: {
      get() {
        return this.formData.documentNumber
      },
      set(value) {
        this.$emit('onChange', { key: 'documentNumber', value: value })
      }
    },

    documentDepartment: {
      get() {
        return this.formData.documentDepartment
      },
      set(value) {
        this.$emit('onChange', { key: 'documentDepartment', value: value })
      }
    },

    documentCreate: {
      get() {
        return this.formData.documentCreate
      },
      set(value) {
        this.$emit('onChange', { key: 'documentCreate', value: value })
      }
    }
  },

  validations: {
    documentType: {
      required
    },

    documentCreate: {
      required
    }
  }
}
</script>
