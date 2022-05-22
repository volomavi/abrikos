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

async function fetchText() {
  const qdata = {
    prompt: "Write a poem",
    temperature: 0.5,
    max_tokens: 64,
    top_p: 1.0,
    frequency_penalty: 0.0,
    presence_penalty: 0.0,
  };

  try { 
    let response = await fetch("https://api.openai.com/v1/engines/text-ada-001/completions", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${process.env.VUE_APP_openAIToken}`,
      },
      body: JSON.stringify(qdata),
    }) 
    return await response.json();

  } catch (error) {
    console.log(error)
  }
  
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
  console.log(answers.choices[0].text)
  console.log(`${markup} markup`)


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
