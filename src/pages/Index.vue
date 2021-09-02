<template>
  <q-page class="container">
    <div v-if ="start">
      <b>你今天的卦是: {{coins}}{{gua}}</b>
      <br/>
      <b>你今天的卦是: {{names[n]}}{{list[n]}}</b>
      <iframe width="100%" :src="'https://zh.wikisource.org/wiki/%E5%91%A8%E6%98%93/' + encodeURI(names[n])"></iframe>
      <button @click="reset()">再來一次</button>
    </div>
    <button v-else class="big" @click="go()">按此開始</button>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'PageIndex',
  data() {
    return {
      start: false,
      n: 0,
      coins: [1,1,1,1,1,1],
      gua: '',
      hash: {
        '111111': '䷀',
        '000000': '䷁',
        '100010': '䷂',
        '010001': '䷃',
        '111010': '䷄', 
        '010111': '䷅',
        '010000': '䷆',
        '000010': '䷇',
        '111011': '䷈',
        '110111': '䷉',
        '111000': '䷊',
        '000111': '䷋',
        '101111': '䷌',
        '111101': '䷍',
        '001000': '䷎',
        '000100': '䷏',
        '100110': '䷐',
        '011001': '䷑'
      },
      list: [
        '䷀', '䷁', '䷂', '䷃', '䷄', '䷅', 
        '䷆', '䷇', '䷈', '䷉', '䷊', '䷋', 
        '䷌', '䷍', '䷎', '䷏', '䷐', '䷑', 

        '䷒', '䷓', '䷔', '䷕', '䷖', '䷗', 
        '䷘', '䷙', '䷚', '䷛', '䷜', '䷝', '䷞', '䷟',
        '䷠', '䷡', '䷢', '䷣', '䷤', '䷥', '䷦', '䷧', '䷨', '䷩', '䷪', '䷫', '䷬', '䷭', '䷮', '䷯',
        '䷰', '䷱', '䷲', '䷳', '䷴', '䷵', '䷶', '䷷', '䷸', '䷹', '䷺', '䷻', '䷼', '䷽', '䷾', '䷿'
      ],
      names: [
        '乾', '坤', '屯', '蒙', '需', '訟', '師', '比', 
        '小畜', '履', '泰', '否', '同人', '大有', '謙', '豫',
        '隨', '蠱', '臨', '觀', '噬嗑', '賁', '剝', '復',
        '无妄', '大畜', '頤', '大過', '坎', '離', '咸', '恆',
        '遯', '大壯', '晉', '明夷', '家人', '睽', '蹇', '解',
        '損', '益', '夬', '姤', '萃', '升', '困', '井',
        '革', '鼎', '震', '艮', '漸', '歸妹', '豐', '旅',
        '巽', '兌', '渙', '節', '中孚', '小過', '既濟', '未濟']
    }
  },
  methods: {
    go() {
      this.start = true
      this.reset()
    },
    reset() {
      this.n = Math.floor(Math.random()*64);
      for (var i = 0; i < this.coins.length; i++) {
        this.coins[i] = Math.floor(Math.random()*2);
      }
      this.gua = this.hash[this.coins.join('')]
    }
  },
  mounted() {
    this.reset()
  }
})
</script>

<style type="text/css" scoped="">

  b {
    font-size: 24px;
  }
  
  iframe {
    height: 75vh;
  }

  .big {
    font-size: 66px;
  }
</style>
