<template>
  <li>
    <base-card>
      <header>
        <h3>{{ prompt }}</h3> 
        <base-button mode="flat" @click="deleteResource(id)">
          Delete
        </base-button>
      </header>
      <p>{{ response }}</p>
      <!-- <nav>
        <a :href="link">Does Google agree?</a>
      </nav> -->
    </base-card>
  </li>
</template>

<script>
export default {
  props: ['id', 'prompt', 'response', 'link'],
  inject: ['deleteResource']
};
</script>

<style>
li {
  margin: auto;
  max-width: 40rem;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  font-size: 1.25rem;
  margin: -0.2rem 0 0.3rem 0;
  color: #004c3f;
}

p {
  margin: 0.5rem 0;
}

a {
  text-decoration: none;
  color: #ce5c00;
}

a:hover,
a:active {
  color: #c89300;
}
</style>
