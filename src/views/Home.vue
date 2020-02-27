
<template>
  <div>
    <div v-show="showText" v-html="text" id="text"></div>
    <div v-show="!showText">Important message!!!</div>
      <hr>
      <button
      ref="btn"
      @click.prevent="showText=!showText"
      :disabled="hideBtn"
      id="btn">
      Show me!
      </button>
      <hr>
      <ul>
        <li v-for="(item, index) in _users" v-bind:key="index">
          {{item.prefix}}{{item.name}}
        </li>
      </ul>
  </div>
</template>

<script>

export default {
  name: 'Home',
  data(){
    return {
      text: '<p>Text string</p><p>Text string</p>',
      showText: false,
      hideBtn: true,
      users: [
        {
          name: 'Ivan',
          gender: 'male'
        }, {
          name: 'Elena',
          gender: 'female'
        }
      ]
    }
  },
  computed: {
    _users() {
      return this.users.map(user => {
        const gender = user.gender
        const prefix = (gender === 'male') ? 'Mr. ' : 'Ms. ';
        user.prefix = prefix
        return user
      })
    }
  },
  created( ) {
    this.enableBtn()
  },
  methods: {
    enableBtn() {
      setTimeout(() => {
        this.hideBtn = false
      }, 1000)
    },
    func1( ) {
      return new Promise(resolve => {
        setTimeout(() => {
          resolve('fetching data')
        }, 2500)
      })
    }
  }
}

</script>
