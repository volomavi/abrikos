<template>
  <h2>Welcome to OpenAI's text-curie-001 AI engine.</h2>

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
import StoredResources from './StoredResources.vue';
import AskQuestion from './AskQuestion.vue';

export default {
  components: {
    StoredResources,
    AskQuestion
  },
  data() {
    return {
      selectedTab: 'ask-question',
      storedResources: [
        {
          id: 'sample0',
          prompt: 'Q: Is the moon made out of cheese?',
          response: 'A: No, the moon is not made out of cheese.'
        },
        {
          id: 'sample2',
          prompt: 'Q: What is your favourite type of food?',
          response:
            'My favourite type of food is anything that I can put in my mouth!'
        }
      ]
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      askQuestion: this.askQuestion,
      deleteResource: this.removeResource
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'ask-question' ? null : 'flat';
    }
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    askQuestion(prompt, response, url) {
      const newQuestion = {
        id: new Date().toISOString(),
        prompt: prompt,
        response: response,
        link: url
      };
      this.storedResources.unshift(newQuestion);
      this.selectedTab = 'stored-resources';
    },
    removeResource(resId) {
      const resIndex = this.storedResources.findIndex(res => res.id === resId);
      this.storedResources.splice(resIndex, 1);
    }
  }
};
</script>
