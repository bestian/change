<template>
  <q-page class="container">
    <div v-if ="start">
      <button @click="reset()" v-show="done">再來一次</button>
      <br/>

      {{coins}}

      <div v-if = "done">
        <b>你今天的卦是: {{coins}}{{gua}} {{name}}</b>
        <br/>
        <b>未來的卦是: {{coins2}}{{gua2}} {{name2}}</b>
      </div>

      <div v-else>
        
        <button @click="p(1,true)">+++太陽</button>
        <button @click="p(1,false)">+-+少陽</button>
        <button @click="p(1,true)">---太陰</button>
        <button @click="p(0,false)">-+-少陰</button>

      </div>

      <div v-if = "name">
        <iframe width="100%" :src="'https://zh.wikisource.org/wiki/%E5%91%A8%E6%98%93/' + encodeURI(name)"></iframe>
        <iframe width="100%" :src="'https://zh.wikisource.org/wiki/%E5%91%A8%E6%98%93/' + encodeURI(name2)"></iframe>
        </div>
      <button @click="reset()" v-show="done">再來一次</button>
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
      done: false,
      n: 0,
      coins: [],
      coins2: [],
      bain: [],
      gua: '',
      gua2: '',
      name: '',
      name2: '',
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
        '011001': '䷑',
        '110000': '䷒',
        '000011': '䷓',
        '100101': '䷔',
        '101001': '䷕',
        '000001': '䷖',
        '100000': '䷗',
        '100111': '䷘',
        '111001': '䷙',
        '100001': '䷚',
        '011110': '䷛',
        '010010': '䷜',
        '101101': '䷝',
        '001110': '䷞',
        '011100': '䷟',
        '001111': '䷠',
        '111100': '䷡',
        '000101': '䷢',
        '101000': '䷣',
        '101011': '䷤',
        '110101': '䷥',
        '001010': '䷦',
        '010100': '䷧',
        '110001': '䷨',
        '100011': '䷩',
        '111110': '䷪',
        '011111': '䷫',
        '000110': '䷬',
        '011000': '䷭',
        '010110': '䷮',
        '011010': '䷮',
        '101110': '䷰',
        '011101': '䷰',
        '100100': '䷲',
        '001001': '䷳',
        '001011': '䷴',
        '110100': '䷵',
        '101100': '䷶',
        '001101': '䷷',
        '011011': '䷸',
        '110110': '䷹',
        '010011': '䷺',
        '110010': '䷻',
        '110011': '䷼',
        '001100': '䷽',
        '101010': '䷾',
        '010101': '䷿'
      },
      list: [
        '䷀', '䷁', '䷂', '䷃', '䷄', '䷅', 
        '䷆', '䷇', '䷈', '䷉', '䷊', '䷋', 
        '䷌', '䷍', '䷎', '䷏', '䷐', '䷑', 
        '䷒', '䷓', '䷔', '䷕', '䷖', '䷗', 
        '䷘', '䷙', '䷚', '䷛', '䷜', '䷝', 
        '䷞', '䷟', '䷠', '䷡', '䷢', '䷣', 
        '䷤', '䷥', '䷦', '䷧', '䷨', '䷩', 
        '䷪', '䷫', '䷬', '䷭', '䷮', '䷯',
        '䷰', '䷱', '䷲', '䷳', '䷴', '䷵', 

        '䷶', '䷷', '䷸', '䷹', '䷺', '䷻', 
        '䷼', '䷽', '䷾', '䷿'
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
    p(k,b) {
      this.coins.push(k)
      this.bain.push(b)
      if (this.coins.length == 6) {
        this.calc()
      }
    },
    calc() {
      this.done = true
      for (var i = 0; i < this.coins.length; i++) {
        if(this.bain[i]) {
          this.coins2[i] = 1 - this.coins[i]
        } else {
          this.coins2[i] = this.coins[i]
        }
      } 
      this.gua = this.hash[this.coins.join('')]
      this.gua2 = this.hash[this.coins2.join('')]
      this.name = this.names[this.list.indexOf(this.gua)]
      this.name2 = this.names[this.list.indexOf(this.gua2)]
    },
    reset() {
      this.coins = []
      this.coins2 = []
      this.bain = []
      this.done = false
      this.n = Math.floor(Math.random()*64);
      /*
      for (var i = 0; i < this.coins.length; i++) {
        this.coins[i] = Math.floor(Math.random()*2);
        this.bain[i] = [true,false,false][Math.floor(Math.random()*3)];
        if(this.bain[i]) {
          this.coins2[i] = 1 - this.coins[i]
        } else {
          this.coins2[i] = this.coins[i]
        }
      } 
      this.gua = this.hash[this.coins.join('')]
      this.gua2 = this.hash[this.coins2.join('')]
      this.name = this.names[this.list.indexOf(this.gua)]
      this.name2 = this.names[this.list.indexOf(this.gua2)]
      */
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
