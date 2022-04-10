<script setup lang="ts">
import { reactive, ref } from 'vue'

interface FormValues {
  email: string
  password: string
  role: string
  terms: boolean
  skills: string[]
}

const tempSkill = ref('')
const passwordError = ref('')

const formValues: FormValues = reactive({
  email: '',
  password: '',
  role: '',
  terms: false,
  skills: [],
})

const handleAddCurrentSkillToSkills = (currentSkill: string) => {
  if (currentSkill.length && !formValues.skills.includes(currentSkill)) {
    formValues.skills.push(currentSkill)
    tempSkill.value = ''
  }
}

const handleAddCurrentSkill = (event: KeyboardEvent): void => {
  let currentSkill = ''

  if (event.key === ',') {
    currentSkill = tempSkill.value.slice(0, -1)
    handleAddCurrentSkillToSkills(currentSkill)
  }
}

const handleDeleteSkill = (event: MouseEvent): string[] => {
  const target = event.target as HTMLDivElement
  const selectedSkill = target.textContent
  const updatedSkills = formValues.skills.filter((skill) => skill !== selectedSkill)

  return (formValues.skills = updatedSkills)
}

const handleSubmit = () => {
  passwordError.value =
    formValues.password.length > 5 ? '' : 'Password must be at least 6 characters'

  if (!passwordError.value) {
    alert(JSON.stringify(formValues, null, 2))
  }
}
</script>

<template>
  <form @submit.prevent="handleSubmit">
    <label for="email">Email:</label>
    <input type="email" required v-model="formValues.email" placeholder="jsmith@gmail.com" />

    <label for="password">Password:</label>
    <input type="password" required v-model="formValues.password" />
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label for="role">Role:</label>
    <select v-model="formValues.role">
      <option disabled value="">Please select one</option>
      <option value="developer">Developer</option>
      <option value="designer">Designer</option>
      <option value="hitman">Hitman</option>
    </select>

    <label>Skills</label>
    <input type="text" v-model="tempSkill" @keyup="handleAddCurrentSkill" />
    <TransitionGroup name="skill">
      <div
        v-for="skill in formValues.skills"
        :key="skill"
        class="pill"
        value="skill"
        @click="handleDeleteSkill"
      >
        {{ skill }}
      </div>
    </TransitionGroup>

    <div>
      <input type="checkbox" required v-model="formValues.terms" />
      <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
      <button>Submit</button>
    </div>
  </form>
</template>

<style>
.skill-enter-active,
.skill-leave-active {
  transition: all 0.5s ease;
}
.skill-enter-from,
.skill-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

form {
  max-width: 420px;
  margin: 30px auto;
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

input[type='checkbox'] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: reactive;
  top: 2px;
}

.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  border-radius: 20px;
  background-color: #42b883;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: white;
  cursor: pointer;
}

button {
  background-color: #42b883;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
  font-weight: bold;
}

.submit {
  text-align: right;
}

.error {
  color: #f05d05;
  margin-top: 10px;
}
</style>
