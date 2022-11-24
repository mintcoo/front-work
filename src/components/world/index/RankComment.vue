<template>
  <div style="height: 100%;">
    <div class="comment-title">익명 게시판</div>
    <div class="scroll-box">
      <li v-for='comment in rankCommentList' :key='comment.id'>
        {{ comment.content }}
      </li>
    </div>
    <input type="text" v-model=inputContent @keyup.enter="createComment">
    <button @click="createComment">작성!</button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'RankComment',
  data() {
    return {
      inputContent: '',
    }
  },
  methods: {
    createComment() {
      console.log('댓글왜안댐')
      if (!this.inputContent.trim()) {
        this.inputContent = ''
        return
      }

      axios({
        method: 'post',
        url: 'http://3.112.101.89/worlds/create_rankcomment/',
        data: {
          'content': this.inputContent
        },
        headers: {
          Authorization: `Token ${this.$store.state.token}`
        }
      })
      .then((res) => {
        this.$store.dispatch('getRankCommentList')
        this.inputContent = ''
      })
    },
    renewCommentList() {
      this.$store.dispatch('getRankCommentList')
    }
  },
  computed: {
    rankCommentList() {
      return this.$store.state.rankComment
    }
  },
  created() {
    this.$store.dispatch('getRankCommentList')
    // setInterval(this.renewCommentList, 3000)
  }
}
</script>

<style scoped>
.comment-title {
  font-size: 35px;
}
.scroll-box {
  text-align: start;
  overflow-y: scroll;
  height: 80%;
}

</style>