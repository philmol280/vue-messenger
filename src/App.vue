<template>
  <div id="app">
    <Container>
      <ChatWindow @send="axios.post('http://188.225.47.187/api/chat/getmessages.php', JSON.stringify($event)).then((response) => {console.log(response);}).catch((error) => {console.log(error);});">
        <div v-for="message in messages" :key="message">
          <ChatMessage :username="message.author" :datetime="message.datetime">{{message.text}}</ChatMessage>
        </div>
      </ChatWindow>
    </Container>
  </div>
</template>

<script>
import axios from 'axios'
import ChatMessage from './components/ChatMessage.vue'
import ChatWindow from './components/ChatWindow.vue'
import Container from './components/Container.vue'

export default {
  name: 'app',
  data() {
  return {messages : []};
  },
  mounted(){
  this.getmessages();
  },
  methods:{
    getmessages(){
    setInterval(() => axios.get('http://188.225.47.187/api/chat/getmessages.php').then(response => {this.messages = response.data.reverse()}), 2000);
    }
  },
  components: {
    ChatMessage, ChatWindow, Container
  }
}
</script>

<style>
#app {
}
body {
  margin: 0;
  background-color: #f9f9fa;
}

</style>
