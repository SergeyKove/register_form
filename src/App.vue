<template>
  <div id="app" class="container">
    <CreateClientForm />
  </div>
</template>

<script>
import CreateClientForm from '@/components/forms/CreateClientForm.vue'

export default {
  name: 'App',

  components: {
    CreateClientForm
  }
}
</script>
