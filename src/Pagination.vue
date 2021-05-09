<style lang="postcss" scoped>
nav.pagination {
  position: relative;
  z-index: 0;
  display: inline-flex;
  box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
}

nav.pagination button {
  margin-left: -1px;
  position: relative;
  display: inline-flex;
  align-items: center;
  padding: 0.5rem 1rem;
  border: 1px solid var(--borderColor);
  background-color: var(--backgroundColor);
  color: var(--textColor);
  font-size: 0.875rem;
  font-weight: 500;

  line-height: 1.25rem;
  transition-property: background-color, border-color, color, fill, stroke,
    opacity, box-shadow, transform;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-duration: 150ms;
}

nav.pagination button:hover {
  color: var(--hoverTextColor);
  background-color: var(--hoverBackgroundColor);
  border-color: var(--hoverBorderColor);
}

nav.pagination button:focus {
  z-index: 10;
  outline: 0;
  box-shadow: 0 0 0 1px var(--textColor);
}

nav.pagination button.active {
  color: var(--selectedTextColor);
  background-color: var(--selectedBackgroundColor);
  border-color: var(--selectedBorderColor);
}

nav.pagination button.spec {
  padding-left: 0.5rem;
  padding-right: 0.5rem;
  color: var(--textColor);
}

nav.pagination button.spec.prev {
  border-top-left-radius: 0.5rem;
  border-bottom-left-radius: 0.5rem;
}

nav button.spec.next {
  border-top-right-radius: 0.5rem;
  border-bottom-right-radius: 0.5rem;
}

nav.pagination button.spec:hover {
  background-color: var(--controlsHoverBorderColor);
}

nav.pagination span {
  margin-left: -1px;
  position: relative;
  display: inline-flex;
  align-items: center;
  padding: 0.5rem 1rem;
  border: 1px solid var(--borderColor);
  background-color: var(--backgroundColor);
  color: var(--textColor);
  font-size: 0.875rem;
  font-weight: 500;
  line-height: 1.25rem;
}

nav.pagination button svg {
  height: 1.25rem;
  width: 1.25rem;
}
</style>

<template>
  <nav class="pagination" :style="computedCssVars">
    <button
      type="button"
      class="spec prev"
      aria-label="Previous"
      @click="setPrev"
    >
      <svg viewBox="0 0 20 20" fill="currentColor">
        <path
          fill-rule="evenodd"
          d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z"
          clip-rule="evenodd"
        />
      </svg>
    </button>

    <template v-for="(button, index) of buttons">
      <button
        type="button"
        :key="'button-' + index"
        v-if="button != '...'"
        :class="button == page ? 'active' : null"
        @click="$emit('change', button)"
      >
        {{ button }}
      </button>
      <span v-else :key="'span-' + index">...</span>
    </template>

    <button type="button" class="spec next" aria-label="Next" @click="setNext">
      <svg viewBox="0 0 20 20" fill="currentColor">
        <path
          fill-rule="evenodd"
          d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
          clip-rule="evenodd"
        />
      </svg>
    </button>
  </nav>
</template>

<script>
export default {
  name: "pagination",
  model: {
    event: "change",
    prop: "page",
  },
  props: {
    page: Number,
    maxPage: Number,
    textColor: { type: String, default: "#4a5568" },
    backgroundColor: { type: String, default: "#fff" },
    borderColor: { type: String, default: "#e2e8f0" },
    selectedTextColor: { type: String, default: "#f7fafc" },
    selectedBackgroundColor: { type: String, default: "#4a5568" },
    selectedBorderColor: { type: String, default: "#e2e8f0" },
    hoverTextColor: { type: String, default: "#f7fafc" },
    hoverBackgroundColor: { type: String, default: "#a0aec0" },
    hoverBorderColor: { type: String, default: "#e2e8f0" },
    controlsHoverBorderColor: { type: String, default: "#cbd5e0" },
  },
  computed: {
    buttons() {
      if (this.maxPage <= 7)
        return Array.from(Array(this.maxPage), (_, i) => i + 1);
      else if (this.page <= 4) return [1, 2, 3, 4, 5, "...", this.maxPage];
      else if (this.page >= this.maxPage - 3)
        return [
          1,
          "...",
          this.maxPage - 4,
          this.maxPage - 3,
          this.maxPage - 2,
          this.maxPage - 1,
          this.maxPage,
        ];
      else
        return [
          1,
          "...",
          this.page - 1,
          this.page,
          this.page + 1,
          "...",
          this.maxPage,
        ];
    },
    computedCssVars() {
      return {
        "--textColor": this.textColor,
        "--backgroundColor": this.backgroundColor,
        "--borderColor": this.borderColor,
        "--selectedTextColor": this.selectedTextColor,
        "--selectedBackgroundColor": this.selectedBackgroundColor,
        "--selectedBorderColor": this.selectedBorderColor,
        "--hoverTextColor": this.hoverTextColor,
        "--hoverBackgroundColor": this.hoverBackgroundColor,
        "--hoverBorderColor": this.hoverBorderColor,
        "--controlsHoverBorderColor": this.controlsHoverBorderColor,
      };
    },
  },
  methods: {
    setPrev() {
      this.$emit("prev", this.page - 1);
      if (this.page > 1) this.$emit("change", this.page - 1);
    },
    setNext() {
      this.$emit("next", this.page + 1);
      if (this.page < this.maxPage) this.$emit("change", this.page + 1);
    },
  },
};
</script>
