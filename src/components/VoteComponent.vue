<template>
  <div>
    <h1>Voting DApp</h1>
    <div>
      <h2>Vote for a Candidate</h2>
      <input v-model="candidate" placeholder="Enter candidate name"/>
      <button @click="voteForCandidate">Vote</button>
    </div>
    <div>
      <h2>Check Votes</h2>
      <input v-model="checkCandidate" placeholder="Enter candidate name"/>
      <button @click="getVotes">Get Votes</button>
      <p v-if="votes !== null">Votes for {{ checkCandidate }}: {{ votes }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'VoteComponent',
  data() {
    return {
      candidate: '',
      checkCandidate: '',
      votes: null
    };
  },
  methods: {
    async voteForCandidate() {
      try {
        const response = await axios.get(`http://localhost:3000/vote/${this.candidate}`);
        alert(response.data);
      } catch (error) {
        console.error(error);
      }
    },
    async getVotes() {
      try {
        const response = await axios.get(`http://localhost:3000/votes/${this.checkCandidate}`);
        this.votes = response.data.split(': ')[1];
      } catch (error) {
        console.error(error);
      }
    }
  }
};
</script>
