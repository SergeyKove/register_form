<template>
  <div>
    <h1>Форма регистрации</h1>

    <form class="flex" @submit.prevent="submit">
      <h2>Основная информация</h2>
      <UserBlockInput :formData="formData" @onChange="onChange" ref="userBlockInput" />

      <BirthdayInput :formData="formData" @onChange="onChange" ref="birthdayInput" />
      <GenderInput :formData="formData" @onChange="onChange" />

      <PhoneInput :formData="formData" @onChange="onChange" ref="phoneInput" />
      <ClientGroupInput :formData="formData" @onChange="onChange" ref="clientGroupInput" />

      <DoctorsInput :formData="formData" @onChange="onChange" />
      <SendSmsInput :formData="formData" @onChange="onChange" />

      <h2>Адрес</h2>
      <AddressBlockInput :formData="formData" @onChange="onChange" ref="addressBlockInput" />

      <h2>Паспорт</h2>
      <DocumentBlockInput :formData="formData" @onChange="onChange" ref="documentBlockInput" />
      
      <small style="margin-bottom: 8px;">*Поле обязательно для заполнения.</small>

      <div class="form-actions">
        <button type="submit" :disabled="submitStatus === 'ERROR'" class="button">
          Отправить форму
        </button>

        <span style="color: red;" v-if="submitStatus === 'ERROR'">Заполните все обязательные поля для отправки формы</span>
        <span v-if="submitStatus === 'PENDING'">Отправка</span>
        <span v-if="submitStatus === 'OK'">Новый клиент успешно создан</span>
      </div>
    </form>
  </div>
</template>

<script>
import UserBlockInput from '@/components/inputBlocks/UserBlockInput.vue'
import BirthdayInput from '@/components/inputs/BirthdayInput.vue'
import GenderInput from '@/components/inputs/GenderInput.vue'
import PhoneInput from '@/components/inputs/PhoneInput.vue'
import ClientGroupInput from '@/components/inputs/ClientGroupInput.vue'
import DoctorsInput from '@/components/inputs/DoctorsInput.vue'
import SendSmsInput from '@/components/inputs/SendSmsInput.vue'

import AddressBlockInput from '@/components/inputBlocks/AddressBlockInput.vue'
import DocumentBlockInput from '@/components/inputBlocks/DocumentBlockInput.vue'

export default {
  components: {
    UserBlockInput,
    BirthdayInput,
    GenderInput,
    PhoneInput,
    ClientGroupInput,
    DoctorsInput,
    SendSmsInput,
    AddressBlockInput,
    DocumentBlockInput
  },

  data() {
    return {
      formData: {
        index: '',
        country: '',
        region: '',
        city: '',
        street: '',
        house: '',
        documentType: '',
        documentSeries: '',
        documentNumber: '',
        documentDepartment: '',
        documentCreate: '',
        lastName: '',
        name: '',
        middleName: '',
        birthday: '',
        clientGroup: [],
        doctors: '',
        gender: '',
        phone: '',
        sendSms: ''
      },
      submitStatus: null,
      validateInputsRefs: [
        'userBlockInput',
        'birthdayInput',
        'phoneInput',
        'addressBlockInput',
        'documentBlockInput',
        'clientGroupInput'
      ]
    }
  },

  methods: {
    submit() {
      this.validateInputsRefs.forEach((item) => {
        const validateItem = this.$refs[item]

        validateItem.$v.$touch()

        if (validateItem.$v.$invalid) {
          this.submitStatus = 'ERROR'
        }
      })

      if (this.submitStatus !== 'ERROR') {
        this.submitStatus = 'PENDING'
        setTimeout(() => {
          this.submitStatus = 'OK'
        }, 500)
      }
    },

    onChange({ key, value }) {
      this.submitStatus = null
      this.$set(this.formData, key, value)
    }
  }
}
</script>

<style scoped>
.form-actions {
  display: flex;
  flex-wrap: wrap;
  padding-bottom: 20px;
}

.button {
  display: inline-block;
  font-weight: 400;
  line-height: 1.5;
  color: #fff;
  text-align: center;
  text-decoration: none;
  vertical-align: middle;
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  user-select: none;
  background-color: #0d6efd;
  border: 1px solid #0d6efd;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  border-radius: 0.25rem;
  transition: background-color 0.15s ease-in-out;
  max-width: 300px;
}

.button:hover {
  color: #fff;
  background-color: #0b5ed7;
  border-color: #0a58ca;
}
</style>
