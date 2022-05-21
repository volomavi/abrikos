<template>
  <div>
    <the-header title="Fun with Curie!"></the-header>
    <the-resources></the-resources>
  </div>
</template>

<script>
import TheHeader from './components/layouts/TheHeader.vue';
import TheResources from './components/learning-resources/TheResources.vue';
export default {
  components: {
    TheHeader,
    TheResources
  }
};

// const qdata = {
//   prompt: 'Write a poem about a dog wearing skis',
//   temperature: 0.5,
//   max_tokens: 64,
//   top_p: 1.0,
//   frequency_penalty: 0.0,
//   presence_penalty: 0.0
// };

// fetch('https://api.openai.com/v1/engines/text-ada-001/completions', {
//   method: 'POST',
//   headers: {
//     'Content-Type': 'application/json',
//     Authorization: `Bearer ${process.env.OPENAI_SECRET}`,
//   },
//   body: JSON.stringify(qdata)
// })
//   .then(response => {
//     if (response.ok) {
//       return response.json();
//     } else {
//       alert('Server returned ' + response.status + ' : ' + response.statusText);
//     }
//   })
  // .then(response => {
  //   this.result = response.body;
  //   this.responseAvailable = true;
  // })
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

* {
  box-sizing: border-box;
}

html {
  font-family: 'Roboto', Helvetica, Arial, sans-serif, sans-serif;
}

body {
  margin: 0;
}

h2 {
  display: flex;
  justify-content: center;
  color: #004c3f;
}
</style>
