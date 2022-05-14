<script setup>
import OvhHeader from './components/OvhHeader.vue'
import TodoListVue from './components/TodoList.vue';
</script>

<template>
  <div class="container">
    <header>
      <img alt="OVH logo" class="logo" src="./assets/ovh.png" width="125" height="125" />

      <div class="wrapper">
        <OvhHeader msg="OVH Todo!" />
      </div>
    </header>

    <main>
      <TodoListVue />
    </main>
  </div>
</template>

<style>
@import './assets/base.css';


.container {
  max-width: 600px;
  margin: 0 auto;
}

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto;
}

a,
.blueOvh {
  text-decoration: none;
  color: hsla(218, 84%, 50%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(218, 100%, 50%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  .logo {
    display: block;
    margin: 0 2rem auto 0;
  }
}
</style>
