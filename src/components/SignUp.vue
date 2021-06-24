<template>
  <form @submit.prevent="handleEvent">
    <label>Email</label>
    <input type="email" required v-model="email" />
    <label>Password</label>
    <input type="password" required v-model="password" />
    <div v-if="passwordError" class="error">
      {{ passwordError }}
    </div>
    <label>Role:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>
    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keydown.shift="addSkill" />

    <ul v-for="skill in skills" :key="skill" class="skills-menu">
      <li @click="deleteSkill(skill)">{{ skill }}</li>
    </ul>

    <div class="terms">
      <input type="checkbox" v-model="terms" required />
      <label>Accept term and conditions</label>
    </div>

    <div class="sumit">
      <button>Submit</button>
    </div>
  </form>
</template>
<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "developer",
      terms: false,
      tempSkill: "",
      skills: [],
      passwordError: "",
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "Shift" && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill))
          this.skills.push(this.tempSkill);

        this.tempSkill = "";
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => item !== skill);
    },
    handleEvent() {
      this.passwordError =
        this.password.length > 5
          ? ""
          : "Password mustb be ar least 6 chars long";

      console.log(this.email);
      console.log(this.password);
      console.log(this.skills);
      console.log(this.role);
    },
  },
};
</script>
<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: #fff;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}

label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"] {
  display: inline;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}

.skills-menu li {
  background-color: #ddd;
  display: inline-block;
  padding: 5px;
  border-radius: 2px;
  cursor: pointer;
  text-transform: uppercase;
}
button {
  background: blue;
  color: white;
  border: 0;
  padding: 10px 20px;
  border-radius: 20px;
  cursor: pointer;
}

.submit {
  text-align: center;
}

.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>