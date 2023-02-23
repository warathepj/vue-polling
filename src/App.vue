<template>
  <div class="h-screen p-6 bg-blue-600">
    <h6 class="text-xl text-blue-200">Programmer Poll</h6>
    <div class="p-3 mt-2 mb-2 rounded-lg bg-sky-300 text-sky-600">
      <h1 v-if="currentArticle">{{ currentArticle.title }}</h1>
      <div v-for="(choice, index) in currentArticle.choices" :key="index">
        <input
          type="radio"
          :id="`choice${index}`"
          :value="index"
          v-model="userChoice"
          :disabled="hasVoted"
        />
        <label :for="`choice${index}`">{{ choice }}</label>
      </div>
    </div>
    <div
      v-if="hasVoted"
      class="p-3 mt-4 mb-2 rounded-lg bg-blue-900 text-blue-300"
    >
      <h2>Results:</h2>
      <div v-for="(choice, index) in currentArticle.choices" :key="index">
        <p>{{ choice }} - {{ results[index] }} vote(s)</p>
      </div>
      <button
        v-if="currentArticleIndex < articles.length - 1"
        @click="nextArticle"
        class="p-1 mt-2 rounded-md bg-blue-300 text-blue-900 hover:bg-blue-600"
      >
        Next Article
      </button>
      <div v-if="currentArticleIndex === articles.length - 1 && hasVoted">
        <p>Thank you for voting!</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      articles: [
        {
          title: "What's your favorite programming language to work with?",
          choices: ["Java", "Python", "C#", "JavaScript"],
          votes: [19, 64, 33, 100],
        },
        {
          title: "What's your preferred development environment?",
          choices: [
            "Visual Studio Code",
            "IntelliJ IDEA",
            "Eclipse",
            "Sublime Text",
          ],
          votes: [172, 14, 3, 18],
        },
        {
          title: "What's your favorite task when coding?",
          choices: [
            "Solving complex problems",
            "Refactoring existing code",
            "Building new features",
            "Writing tests",
          ],
          votes: [55, 25, 78, 19],
        },
      ],
      currentArticleIndex: 0,
      userChoice: null,
    };
  },
  computed: {
    currentArticle() {
      return this.articles[this.currentArticleIndex];
    },
    results() {
      return this.currentArticle.votes.map((voteCount, index) => {
        return voteCount + (this.userChoice === index ? 1 : 0);
      });
    },
    hasVoted() {
      return this.userChoice !== null;
    },
  },
  methods: {
    nextArticle() {
      this.currentArticleIndex++;
      this.userChoice = null;
    },
  },
};
</script>


