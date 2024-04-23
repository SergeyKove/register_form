<template>
  <div class="checkbox" style="display: flex">
    <input id="sendSms" type="checkbox" v-model="sendSms" class="custom-checkbox" />
    <label for="sendSms">Не отправлять смс</label>
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
    sendSms: {
      get() {
        return this.formData.sendSms
      },
      set(value) {
        this.$emit('onChange', { key: 'sendSms', value: value })
      }
    }
  }
}
</script>
