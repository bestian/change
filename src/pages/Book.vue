<template>
  <q-page class="container">
    <div class="inline" v-for = "(l, idx) in list" :key="l">
      <h3>
        <router-link :to = "'/detail/' + idx">
          {{l}}{{names[idx]}}
        </router-link>
      </h3>
    </div>
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
      list: [
        '䷀', '䷁', '䷂', '䷃', '䷄', '䷅', '䷆', '䷇', '䷈', '䷉', '䷊', '䷋', '䷌', '䷍', '䷎', '䷏',
        '䷐', '䷑', '䷒', '䷓', '䷔', '䷕', '䷖', '䷗', '䷘', '䷙', '䷚', '䷛', '䷜', '䷝', '䷞', '䷟',
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

  .inline {
    display: inline-block;
  }

  a {
    text-decoration: none;
  }
</style>
