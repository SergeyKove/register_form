<template>
  <div class="text-field">
    <label class="text-field__label" for="clientGroup">Группа клиентов*</label>

    <DropdownMenu
      id="clientGroup"
      :title="selectedTitle"
      :class="{ 'text-field__input_invalid': $v.clientGroup.$error }"
    >
      <option
        v-for="item in items"
        :key="item"
        @click.prevent.stop="() => onSelect(item)"
        class="option"
        :class="{ option_active: clientGroup.includes(item) }"
      >
        {{ item }}
      </option>
    </DropdownMenu>

    <span v-if="$v.clientGroup.$error" class="text-field__message">
      <small> Поле обязательно для заполнения </small>
    </span>
  </div>
</template>

<script>
import DropdownMenu from '@/components/ui/DropdownMenu.vue'
import { required } from 'vuelidate/lib/validators'

export default {
  components: {
    DropdownMenu
  },

  data() {
    return {
      items: ['VIP', 'Проблемные', 'ОМС']
    }
  },

  props: {
    formData: {
      type: Object,
      default: () => ({})
    }
  },

  computed: {
    clientGroup: {
      get() {
        return this.formData.clientGroup
      },
      set(value) {
        this.$emit('onChange', { key: 'clientGroup', value })
      }
    },

    selectedTitle() {
      return this.clientGroup.join(', ')
    }
  },

  methods: {
    onSelect(value) {
      if (this.clientGroup.includes(value)) {
        this.clientGroup = this.clientGroup.filter((item) => item !== value)
      } else {
        this.clientGroup = [...this.clientGroup, value]
      }
      this.$v.clientGroup.$touch()
    }
  },

  validations: {
    clientGroup: {
      required
    }
  }
}
</script>

<style scoped>
.option {
  width: 100%;
  padding: 0 15px;
  cursor: pointer;
}

.option:hover {
  background-color: #0b76ef;
  color: white;
}

.option_active {
  background-color: #0b76ef;
  color: white;
}
</style>