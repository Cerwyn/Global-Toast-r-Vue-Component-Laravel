<template>
  <div id="toast-container" class="toast-container toast-top-right">
    <div class="toast toast-error" aria-live="assertive" style="display: block;" v-show="show">
      <div class="toast-title">{{ titleToast }}</div>
      <div class="toast-message">{{ bodyToast }}</div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["title", "body"],

  data() {
    return {
      titleToast: "",
      bodyToast: "",
      show: false
    };
  },

  created() {
    if (this.title) {
      this.flash(this.title, this.body);
    }

    window.events.$on("toast-error", (title, body) => {
      this.flash(title, body);
    });
  },

  methods: {
    flash(title, body) {
      this.titleToast = title;
      this.bodyToast = body;

      this.show = true;

      this.hide();
    },

    hide() {
      setTimeout(() => {
        this.show = false;
      }, 2000);
    }
  }
};
</script>

<style>
@import "/css/toastr.css";
</style>