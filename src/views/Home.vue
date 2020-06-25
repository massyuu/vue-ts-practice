<template>
  <div class="home">
    <p>{{ greetText }}</p>
    <p>挨拶した回数 : {{ count }}回</p>
    <p v-if="isRegulars">いつもありがとうございます</p>
    <MyButton :greet="greetText" @click="onMyButtonClicked">挨拶する</MyButton>
    <ResetButton initialValue="hello world" v-model="greetText"></ResetButton>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Watch } from "vue-property-decorator";
import MyButton from "@/components/MyButton.vue";
import ResetButton from "@/components/ResetButton.vue";

@Component({
  components: {
    MyButton,
    ResetButton
  }
})
export default class Home extends Vue {
  public greetText = "hello world";

  // 下位コンポーネントから持ってくる値
  private count = 0;

  // 算出プロパティ
  public get isRegulars(): boolean {
    return this.count >= 5;
  }

  //監視
  @Watch('count')
  public countChanged() {
    // メソッド名は任意。監視対象の指定が大切。
    if(this.count === 5) {
      alert("常連になりました");
    }
  }

  public onMyButtonClicked(count: number) {
    this.count = count;
    this.greetText = "こんにちは";
  }
}
</script>
