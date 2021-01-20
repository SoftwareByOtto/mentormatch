<template>
  <div class="container">
    <h1 class="title">mentor<span style="color: grey">match</span></h1>
    <h2>meet your match</h2>
    <hr/>
    <h1>add mentor</h1>
    <form @submit.prevent="addMentor(mentorSkill, mentorName)">
      <input type="text" v-model="mentorName" placeholder="name">
      <input type="text" v-model="mentorSkill" placeholder="skill">
      <button>Submit</button>
    </form>
    <h1>add mentee</h1>
    <form @submit.prevent="addMentee(menteeSkill, menteeName)">
      <input type="text" v-model="menteeName" placeholder="name">
      <input type="text" v-model="menteeSkill" placeholder="skill">
      <button>Submit</button>
    </form>
    <h1>mentors</h1>
    <!-- {{mentors}} -->
    <div class="flex">
      <div class="item orange" v-for="mentor in mentors">
        <h2>{{mentor.mentorName}}</h2>
        <i>can offer</i>
        <p>{{mentor.mentorSkill}}</p>
      </div>
    </div>
    <h1>mentees</h1>
    <!-- {{mentees}} -->
    <div class="flex">
      <div class="item blue" v-for="mentee in mentees">
        <h2>{{mentee.menteeName}}</h2>
        <i>is looking for</i>
        <p>{{mentee.menteeSkill}}</p>
      </div>
    </div>
    <h1>matches</h1>
    <!-- {{matches}} -->
    <div class="flex">
      <div class="item purple" v-for="match in matches">
        <div class="skill">SKILL</div>
        <h2>{{match.skill}}</h2>
        <h3>Mentors</h3>
        <div v-for="mentor in match.mentors">
          {{mentor}}
        </div>
        <div v-if="!match.mentors.length">No mentors!</div>
        <h3>Mentees</h3>
        <div v-for="mentee in match.mentees">
          {{mentee}}
        </div>
        <div v-if="!match.mentees.length">No mentees!</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      mentorName: '',
      mentorSkill: '',
      menteeName: '',
      mentorSkill: '',
      mentors: [],
      mentees: []
    }
  },
  methods: {
    addMentor(mentorSkill, mentorName) {
      this.mentors.push({mentorSkill, mentorName})
    },
    addMentee(menteeSkill, menteeName) {
      this.mentees.push({menteeSkill, menteeName})
    },
  },
  computed: {
    matches() {
      const skills = [...new Set([
        ...this.mentors.map(m => m.mentorSkill),
        ...this.mentees.map(m => m.menteeSkill)
      ])]
      return skills.map(skill => ({
        skill: skill,
        mentors: this.mentors.filter(m => m.mentorSkill === skill).map(m => m.mentorName),
        mentees: this.mentees.filter(m => m.menteeSkill === skill).map(m => m.menteeName)
      }))
    }
  }
}
</script>

<style>
  .container {
    padding: 40px;
    margin-left: 10%;
    background: linear-gradient(to right, rgba(255,255,255,1) 0%, rgba(246,246,246,1) 47%, rgba(237,237,237,1) 100%);
  }
  .flex {
    display: flex;
    flex-wrap: wrap;
    padding: 20px;
  }
  .item, form, input {
    padding: 30px;
    margin: 10px;
  }
  .item {
    border-radius: 15px 0 30px 0;
  }
  input, button {
    font-size: 20px;
    height: 50px;
  }
  button {
    background-color: gold;
  }
  .item h2 {
    margin: 10px;
    text-align: center;
  }
  .title {
    text-align: center;
    padding: 20px;
    font-size: 500%;
    border-radius: 15px 0 30px 0;
    background-color: rgb(196, 196, 223);
    width: 150px;
    margin-bottom: 30px;
  }
  .skill {
    font-size: 10px;
    text-align: center;
    font-weight: bold;
  }
  .blue {
    background-color: aquamarine;
  }
  .purple {
    background-color: rgb(174, 106, 201);
  }
  .orange {
    background-color: rgb(221, 152, 87);
  }
</style>
