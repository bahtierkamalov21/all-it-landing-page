<template lang="pug">
div
  dialog(class="bottom-sheet" ref="modal" :open="open")
    v-card(class="card pa-4 pr-2" color="menuBackground" elevation="0" :class="{ 'active' : active }")
      v-col(class="top d-flex justify-space-between align-center")
        v-row(class="align-center")
          v-chip(color="costumBlue" class="font-weight-bold px-6") {{ $t("menu") }}
          switch-language(class="ml-2")
          switch-theme(class="ml-4")
        v-btn(icon @click="setAndCloseOpen()")
          v-icon mdi-close
</template>

<script>
import SwitchTheme from "@/components/SwitchTheme";
import SwitchLanguage from "@/components/SwitchLanguage";

export default {
  name: "TopSheetMenu",
  data() {
    return {
      active: false,
    };
  },
  components: { SwitchTheme, SwitchLanguage },
  watch: {
    open() {
      this.setOpen();
    },
  },
  props: {
    open: Boolean,
  },
  mounted() {
    window.addEventListener("click", (event) => {
      event.target === this.$refs.modal ? this.setAndCloseOpen() : null;
    });
  },
  methods: {
    setOpen() {
      this.$emit("setOpen", this.open);
    },
    setAndCloseOpen() {
      this.active = !this.active;
      setTimeout(() => {
        this.active = !this.active;
        this.$emit("setOpen", !this.open);
      }, 200);
    },
  },
};
</script>

<style scoped lang="scss">
.bottom-sheet {
  position: fixed;
  width: 100vw;
  height: 100vh;
  z-index: 120;
  left: 0;
  border: none;
  background-color: rgba(0, 0, 0, 0.25);
  top: 0;
  overflow: hidden;
}

.avatar {
  border-radius: 50%;
  overflow: hidden;
  width: 52px;
  height: 52px;
  cursor: pointer;

  & > *:last-child {
    font-size: 52px;
  }
}

.bottom-sheet[open] > .card {
  animation: down 0.2s linear forwards;
}

.card {
  border-radius: 0 0 24px 24px;
  box-shadow: 0 0 5px 0 rgba(0, 0, 0, 0.25) !important;
}

.top {
  & > *:first-child {
    & > *:first-child {
      color: #ffffff;
    }
  }
}

.active {
  animation: down-leave 0.2s linear forwards !important;
}

@keyframes down {
  from {
    transform: translateY(-100%);
  }

  to {
    transform: translateY(0);
  }
}

@keyframes down-leave {
  from {
    transform: translateY(0);
  }

  to {
    transform: translateY(-100%);
  }
}
</style>
