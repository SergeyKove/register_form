<template>
  <section
    class="text-field__input dropDownMenuWrapper"
    :class="{ 'text-field__input_focus': isOpen }"
  >
    <button class="dropDownMenuButton" ref="menu" @click="openClose">
      {{ title }}
    </button>

    <div class="iconWrapper">
      <div class="triangle_down"></div>
    </div>

    <section class="dropdownMenu" v-if="isOpen">
      <slot />
    </section>
  </section>
</template>

<script>
export default {
  props: {
    title: String
  },

  data() {
    return {
      isOpen: false
    }
  },

  methods: {
    openClose() {
      var _this = this

      const closeListerner = (e) => {
        // Check if user clicks outside of the menu
        // true — close the menu and remove EventListener
        if (_this.catchOutsideClick(e, _this.$refs.menu))
          window.removeEventListener('click', closeListerner), (_this.isOpen = false)
      }

      // Add event listener to watch clicks outside the menu
      window.addEventListener('click', closeListerner)

      // Close if open and vice versa
      this.isOpen = !this.isOpen
    },

    catchOutsideClick(event, dropdown) {
      // When user clicks menu — do nothing
      if (dropdown == event.target) return false
      if (this.isOpen && dropdown != event.target) return true
    }
  }
}
</script>

<style scoped>
.triangle_down {
  position: relative;
  top: -5px;
  content: '';
  display: inline-block;
  width: 7px;
  height: 7px;
  border-right: 2px solid black;
  border-top: 2px solid black;
  transform: rotate(135deg);
  margin-right: 0.5em;
  margin-left: 1em;
}
.dropDownMenuWrapper {
  position: relative;
}
.dropDownMenuWrapper * {
  box-sizing: border-box;
  text-align: left;
}

.dropDownMenuButton {
  border: none;
  font-size: inherit;
  background: none;
  outline: none;
  border-radius: 4px;
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  padding: 0.375rem 0.75rem;
  margin: 0;
  line-height: 1;
  width: 100%;
  height: 100%;
  z-index: 2;
  cursor: pointer;
}

/* menu */
.dropdownMenu {
  position: absolute;
  top: 36px;
  right: 0;
  width: 100%;
  min-width: 300px;
  min-height: 10px;
  border: 1px solid #eee;
  box-shadow: 10px 10px 0 0 rgba(black, 0.03);
  background: white;
}

/* icon */
.iconWrapper {
  width: 25px;
  height: 25px;
  position: absolute;
  right: 3px;
  top: 50%;
  transform: translate(0, -50%);
  z-index: 1;
}
</style>
