<template>
  <button @click="onClick">
    <slot></slot>
  </button>
</template>

<script lang="ts">
import { Component, Prop, Vue, Emit } from "vue-property-decorator";

@Component
export default class MyButton extends Vue {
  // 上位コンポーネントに渡す値
  private count = 0;

  @Prop()
  public greet?: string;

  @Emit()
  public click(count: number) {}

  public onClick() {
    alert(this.greet);
    this.count++;
    this.click(this.count);
  }
}
</script>
