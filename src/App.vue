<template>
  <div id="app">
      <div class="container">
        <div class="toolbar">
          <button v-if="mode" type="button" @click="selectAll">Tout séléctionner ({{ contacts.length }})</button>
          <button v-else type="button" @click="deselectAll">Tout déséléctionner ({{ contacts.length }})</button>
        </div>
        <div class="card" v-for="(contact, i) in contacts" :key="'lol' + i">
          <input type="checkbox" :checked="contact.checked">
          <img class="avatar" :src="contact.image" alt="">
          <div class="card-contact">
            <span>{{ contact.fullName }}</span>
            <span>{{ contact.email }}</span>
          </div>
        </div>
      </div>
  </div>
</template>

<script>
import fake from '@/assets/fake.json';

export default {
  name: 'App',
  data() {
    return {
      contacts: [],
      mode: true
    }
  },
  methods: {
    selectAll() {
      this.contacts.map((c) => c.checked = true);
      this.mode = false;
    },
    deselectAll() {
      this.contacts.map((c) => c.checked = false);
      this.mode = true;
    }
  },
  mounted() {
    fake.forEach((c) => {
      this.contacts.push({ ...c, checked: false});
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.container {
  width: 90%;
  margin: 0 auto;
}

.toolbox {

}

.card {
  display: flex;
  margin: 1em 0;
  padding: 1em;
  background: rgba(0,0, 0, 0.1);
}

.card-contact {
  display: flex;
  flex-flow: column nowrap;
}

.avatar {
  width: 48px;
  height:48px;
  border-radius: 5px;
  margin-right: 1em;
  margin-left: 1em;
}
</style>
