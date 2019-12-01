<template lang="pug">
.hello
  h1 {{ msg }}
  .button(v-if="!showCamera", @click="buttonClicked")
    p(style="user-select: none;") Click Me!
  camera(v-if="showCamera")
</template>

<script>
// eslint-disable 
import Camera from './Camera'
export default {
  name: 'HelloWorld',
  components: {
    Camera
  },
  data() {
    return {
      msg: 'eMoTiOnS',
      showCamera: false
    }
  },
  methods: {
    buttonClicked() {
    fetch("https://lhd2019.azurewebsites.net/api/GetSpotifyOuthURL?code=nidsqbrTTU20uP06EHsxoqbzhaFvkC8FFoArDGzurRbqjcdP3IYwgw==",
      {
        mode: 'cors',
        headers: {
          'Access-Control-Allow-Origin':'*'
        }
      }).then(response => {
      if (response.status !== 200) {
        return
      }
      response.json().then(data => {
        window.location = data.url
      })
      })
    }
  },
  mounted() {
    const vars = {};
    window.location.href.replace(/[?&]+([^=&]+)=([^&]*)/gi, function(m,key,value) {
        vars[key] = value;
    });
    if (vars['code']) {
      this.showCamera = true
    }
  }
}
</script>

<style lang="scss" scoped>
.button {
  width: 120px;
  height : 50px;
  background-color: lightskyblue;
  border-radius: 5px;
  align-self: center;

  &:hover {
    cursor: pointer;
    background-color: #85C1E9
  }
}
.hello {
  display: flex;
  flex-direction: column;
}
</style>
