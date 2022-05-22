<template>
  <div class="introduction">
    <h2>Welcome to OpenAI's text-curie-001 AI engine.</h2>
    <p>
      OpenAI is an artificial intelligence (AI) research laboratory consisting
      of the for-profit corporation OpenAI LP and its parent company, the
      non-profit OpenAI Inc. The company, considered a competitor to DeepMind,
      conducts research in the field of AI with the stated goal of promoting and
      developing friendly AI in a way that benefits humanity as a whole.
    </p>
  </div>
  <base-card>
    <base-button
      @click="setSelectedTab('ask-question')"
      :mode="addResButtonMode"
      >Ask a question!</base-button
    >
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResButtonMode"
      >Previously asked questions</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from "./StoredResources.vue";
import AskQuestion from "./AskQuestion.vue";

export default {
  components: {
    StoredResources,
    AskQuestion,
  },
  data() {
    return {
      selectedTab: "ask-question",
      storedResources: [
        {
          id: "sample0",
          prompt: "Q: Is the moon made out of cheese?",
          response: "A: No, the moon is not made out of cheese.",
        },
        {
          id: "sample1",
          prompt: "Q: Whats heavier, a pound of feathers or a pound of nails?",
          response:
            "A: Nails are heavier.",
        },
      ],
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      askQuestion: this.askQuestion,
      deleteResource: this.removeResource,
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === "stored-resources" ? null : "flat";
    },
    addResButtonMode() {
      return this.selectedTab === "ask-question" ? null : "flat";
    },
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    async fetchText(prompt) {
      const qdata = {
        prompt: prompt,
        temperature: 0.5,
        max_tokens: 64,
        top_p: 1.0,
        frequency_penalty: 0.0,
        presence_penalty: 0.0,
      };
      try {
        let response = await fetch(
          "https://api.openai.com/v1/engines/text-curie-001/completions",
          {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
              Authorization: `Bearer ${process.env.VUE_APP_openAIToken}`,
            },
            body: JSON.stringify(qdata),
          }
        );
        return await response.json();
      } catch (error) {
        console.log(error);
      }
    },
    async askQuestion(prompt) {
      let answers = await this.fetchText(prompt);
      const newQuestion = {
        id: new Date().toISOString(),
        prompt: `Q: ${prompt}`,
        response: `A: ${answers.choices[0].text}`,
      };
      this.storedResources.unshift(newQuestion);
      this.selectedTab = "stored-resources";
    },

    removeResource(resId) {
      const resIndex = this.storedResources.findIndex(
        (res) => res.id === resId
      );
      this.storedResources.splice(resIndex, 1);
    },
  },
};
</script>

<style scoped>
.introduction {
  display: flex;
  flex-direction: column;
  max-width: 700px;
  margin: 0 auto;
}
</style>
