<template>
  <div class="home">
    <p>{{greetText}}</p>
    <p>挨拶した回数: {{count}}</p>
    <p v-if='isRegulars'>いつもありがとうございます。</p>
    <p>
      <MyButton :greet="greetText" @clicked="onMyButtonClicked" class='my-button'>挨拶する</MyButton>
    </p>
    <p>
      <ResetButton initialValue='Hello' v-model="greetText"></ResetButton>
    </p> 
  </div>
</template>

<script lang="ts">
// @ is an alias to /src
import { Component, Vue, Watch } from 'vue-property-decorator';
import MyButton from '@/components/MyButton.vue';
import ResetButton from '@/components/ResetButton.vue';

@Component({
  components: {
    MyButton,
    ResetButton,
  },
})

export default class Home extends Vue {
  private count: number = 0;
  public greetText: string = 'HELL ON';

  public get isRegulars(): boolean {
    return this.count >= 5
  }

  @Watch('count')
  public countChanged(){
    if(this.count === 5) alert('you became a regulars');
  }

  public onMyButtonClicked(count: number) {
    this.count = count;
    this.greetText = 'こんにちは';
  } 
}

</script>
