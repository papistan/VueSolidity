<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h3>{{ showAccount }}</h3>
  </div>
</template>

<script>
import web3 from 'web3'


let provider = new Web3(new Web3.providers.HttpProvider('http://localhost:8545'))

provider.eth.defaultAccount = provider.eth.accounts[0]

let MyContract = provider.eth.contract([{"constant":true,"inputs":[],"name":"get","outputs":[{"name":"","type":"bytes32"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"x","type":"bytes32"}],"name":"set","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"}]);

let contract = MyContract.at('0x43ea5b0ee2a81dcef4c1f794afa697f2b27ce680')


export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Current Account:: '
    }
  },
  computed: {
    showAccount: function() {
      return this.msg + provider.eth.defaultAccount
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
