<template>
  <h1>20. Write a function which filter users who has scoresGreaterThan85, Write a function which addUser to the user array only if the user does not exist. Write a function which addUserSkill which can add skill to a user only if the user exist. Write a function which editUser if the user exist in the users array.</h1>
  <div class="example">
    <code><pre>
const users = [
{
	name:'Brook', 
	scores:75,
	skills:['HTM', 'CSS', 'JS'],
	age:16
},
{
	name:'Alex', 
	scores:80,
	skills:['HTM', 'CSS', 'JS'],
	age:18
}, 
{
	name:'David', 
	scores:75,
	skills:['HTM', 'CSS'],
	age:22
}, 
{
	name:'John', 
	scores:85,
	skills:['HTM'],
	age:25
},
{
	name:'Sara',
	scores:95,
	skills:['HTM', 'CSS', 'JS'],
	age: 26
},
{
	name:'Martha', 
	scores:80,
	skills:['HTM', 'CSS', 'JS'],
	age:18
},
{
	name:'Thomas',
	scores:90,
	skills:['HTM', 'CSS', 'JS'],
	age:20
}
];
    </pre></code>
  </div>
  <component :is="modal"/>
  <div style="display: grid; column-gap: 10px; grid-template-columns: repeat(4, 1fr); font-weight: bolder;">
      <span>Name</span>
      <span>Score</span>
      <span>Skills</span>
      <span>Age</span>
  </div>
  <ul style="margin-inline-start: 0;">
    <li v-for="u in filterGreaterThan(users, limit)" :key="u.name" style="display: grid; column-gap: 10px; grid-template-columns: repeat(4, 1fr);">
      <span>{{ u.name }}</span>
      <span>{{ u.scores }}</span>
      <span>{{ u.skills }}</span>
      <span>{{ u.age }}</span>
    </li>
  </ul>
  <fieldset style="display: flex; flex-wrap: wrap; column-gap: 6px;">
    <legend>Options</legend>
    <label style="flex: 1 1 100%;">Filter users with scores over: <input type="number" v-model="limit"/></label>
    <button @click="addUser">Add User</button>
    <button @click="addUser">Add Skill</button>
    <button @click="addUser">Edit User</button>
  </fieldset>
</template>
<script setup lang="tsx">
import { defineComponent, ref, watch } from 'vue';
interface Iuser {
  name: string,
  scores: number,
  skills: string[],
  age: number
}
const SKILLS = ['HTML', 'CSS', 'JS']
const limit = ref(0)
const modal = ref()
const users = ref<Iuser[]>([
{
	name:'Brook', 
	scores:75,
	skills:['HTM', 'CSS', 'JS'],
	age:16
},
{
	name:'Alex', 
	scores:80,
	skills:['HTM', 'CSS', 'JS'],
	age:18
}, 
{
	name:'David', 
	scores:75,
	skills:['HTM', 'CSS'],
	age:22
}, 
{
	name:'John', 
	scores:85,
	skills:['HTM'],
	age:25
},
{
	name:'Sara',
	scores:95,
	skills:['HTM', 'CSS', 'JS'],
	age: 26
},
{
	name:'Martha', 
	scores:80,
	skills:['HTM', 'CSS', 'JS'],
	age:18
},
{
	name:'Thomas',
	scores:90,
	skills:['HTM', 'CSS', 'JS'],
	age:20
}
])
const AddUser = defineComponent({
  setup(props: { msg: string; list: Iuser[] }, { emit }) {
    // use Composition API here like in <script setup>
    const selected = ref(0)
    const isVisible = ref(true)
    const [userMinAge, userMaxAge] = [6, 120]
    const [scoreMin, scoreMax] = [0, 100]
    const user = ref<Iuser>({
      name: '',
      scores: 0,
      skills: ['HTML'],
      age: userMinAge
    })

    function isUserSkill(skill: string){
      if (!user.value.skills.length) return false
      return user.value.skills.includes(skill)
    }
    function checkIfInRange(num: number, min: number, max: number) {
      if (num < min) return min
      if (num > max) return max
      return num
    }
    const onClick = (e: void) => {
      isVisible.value = false
      emit('selected', user.value)
    }
    const onClose = () => {
      isVisible.value = false
      emit('close')
    }
    return () => {
      // render function or JSX
      return (
        <dialog style={{display: isVisible.value ? 'flex': 'none'}}>
          <span class="close" onClick={ onClose }/>
          <form class="flex-column" onSubmit={(e) => onClick(e.preventDefault())}>
            <h3>{ props.msg }</h3>
            <label class="required" for="name">Name:</label>
            <input type="text" name="name" v-model={ user.value.name } id="name" required/>
            <span>
              <label class="required" for="scores">Scores:</label>
              <input type="number" v-model={ user.value.scores } id="scores" onInput={() => user.value.scores = checkIfInRange(user.value.scores, scoreMin, scoreMax)} required/>
            </span>
            <label for="skills">Skills:</label>
            <select v-model={ user.value.skills } id="skills" multiple>
              { SKILLS.map(e => <option selected={isUserSkill(e)}>{ e }</option>) }
            </select>
            <span>
              <label class="required" for="age">Age <span class="extra-message">(6 - 120)</span>:</label>
              <input type="number" v-model={ user.value.age } id="age" min={userMinAge} max={userMaxAge} onChange={() => user.value.age = checkIfInRange(user.value.age, userMinAge, userMaxAge)} required/>
            </span>
            <button style={{width:'100%'}}>Add user</button>
          </form>
        </dialog>
      )
    }
  },
  // manual runtime props declaration is currently still needed.
  props: ['msg', 'list'],
  emits: ['selected', 'close']
})
function filterGreaterThan(arr: Iuser[], limit: number){
  return arr.filter(u => u.scores >= limit)
}
function closeModal(){ modal.value = null }
function addUser(){
  const checkIfExits = (user: Iuser) => {
    modal.value = null
    const isPresent = users.value.find(u => u.name.toLowerCase() === user.name.toLowerCase())
    if (!isPresent) return users.value.push(user)
    return alert(`User ${user.name} already exist!`)
  }
  modal.value = <AddUser msg={'Add user'} list={users.value} onSelected={checkIfExits} onClose={closeModal}/>
}
</script>