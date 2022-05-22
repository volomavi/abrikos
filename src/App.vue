<template>
  <div>
    <the-header title="Fun with Curie!"></the-header>
    <the-resources></the-resources>
  </div>
  <div class="container"></div>
</template>

<script>
import TheHeader from "./components/layouts/TheHeader.vue";
import TheResources from "./components/learning-resources/TheResources.vue";
export default {
  components: {
    TheHeader,
    TheResources,
  },
};

// let jsonResponse

async function fetchText() {
  const qdata = {
    prompt: "Write a poem",
    temperature: 0.5,
    max_tokens: 64,
    top_p: 1.0,
    frequency_penalty: 0.0,
    presence_penalty: 0.0,
  };

  fetch("https://api.openai.com/v1/engines/text-ada-001/completions", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${process.env.VUE_APP_openAIToken}`,
    },
    body: JSON.stringify(qdata),
  }).then((response) => {
    if (response.ok) {
      // jsonResponse = response.json();
      // console.log(response.json())
      return response.json();
    } else {
      alert("Server returned " + response.status + " : " + response.statusText);
    }
  });
}

async function showText() {
  let answers = await fetchText();
  let markup = "hi";
  // answers.forEach((answer) => {
  //   let markupSegment = `<div class="reply">
  //                         <p>${answer[0].text}2</p>;
  //                         <p>${answer[0]}3</p>;
  //                         <p>${answer}3</p>;
  //                         <p>${answers}3</p>;
  //                         <p>3</p>;
                          

  //                       </div>`
  //   markup += markupSegment;                        
  // });
  console.log(`${answers} answers`)
  console.log(`${markup} markup`)
  // console.log(jsonResponse)


  // markup += answers.id
  // let container = document.querySelector('.container');
  // if (markup){
  //   container.innerHTML = `${markup}hi`;
  //   console.log('markup hits')
  // } else {
  // container.innerHTML = `bye`;
  //   console.log('markup doesnt')

  // }

}

showText()
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap");

* {
  box-sizing: border-box;
}

html {
  font-family: "Roboto", Helvetica, Arial, sans-serif, sans-serif;
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
