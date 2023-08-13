<template>
  <h1>18. The following todoList has three tasks. Create an addTask, removeTask, editTask, toggleTask, toggleAll, removeAll functions to modify the todoList.</h1>
  <div class="example">
    <code><pre>
const todoList = [
{
	task:'Prepare JS Test',
	time:'4/3/2019 8:30',
	completed:true
	
},
{
	task:'Give JS Test',
	time:'4/3/2019 10:00',
	completed:false
	
},
{
	task:'Assess Test Result',
	time:'4/3/2019 1:00',
	completed:false
	
}]
    </pre></code>
  </div>
  <component :is="dynamicCompon"/>
  <ul class="toDoList">
    <li class="task" v-for="(t, index) in todoList" :key="t.time">
      <input type="checkbox" v-model="t.completed">
      <p>{{ t.task }}</p>
      <span>{{ t.time }}</span>
      <button class="remove" @click="remove(index)">x</button>
    </li>
  </ul>
  <fieldset>
    <legend>Options</legend>
    <button @click="addTask()">addTask</button>
    <button @click="editTask()">editTask</button>
    <button @click="toggleTask()">toggleTask</button>
    <button @click="toggleAll()">toggleAll</button>
    <button @click="removeTask()">removeTask</button>
    <button @click="removeAll()">removeAll</button>
  </fieldset>
</template>
<script setup lang="tsx">
import { ref, defineComponent, computed, watch, onMounted } from 'vue'
interface ItoDo {
  task: string,
  time: string,
  completed: boolean
}
const todoList = ref<ItoDo[]>([
{
	task:'Prepare JS Test',
	time:'4/3/2019 8:30',
	completed:true
},
{
	task:'Give JS Test',
	time:'4/3/2019 10:00',
	completed:false
},
{
	task:'Assess Test Result',
	time:'4/3/2019 1:00',
	completed:false
}])
const dynamicCompon = ref()

const SelectTask = defineComponent({
  setup(props: { msg: string; list: ItoDo[] }, { emit }) {
    // use Composition API here like in <script setup>
    const selected = ref(0)
    const isVisible = ref(true)
   
    const onChange = (v: Event) => selected.value = parseInt((v?.target as HTMLInputElement).value)
    const onClick = () => {
      isVisible.value = false
      emit('selected', selected.value)
    }
    const onClose = () => {
      isVisible.value = false
      emit('close')
    }
    return () => {
      // render function or JSX
      return (
        <dialog class="flex-column" style={{display: isVisible.value ? 'flex': 'none'}}>
          <span class="close" onClick={ onClose }/>
          <h3>{ props.msg }</h3>
          <select onChange={ onChange }>
            { props.list.map((e, index: number) => <option value={index}>{index + 1}</option> ) }
          </select>
          <button style={{width:'100%'}} onClick={ onClick }>Confirm</button>
        </dialog>
      )
    }
  },
  // manual runtime props declaration is currently still needed.
  props: ['msg', 'list'],
  emits: ['selected', 'close']
})
const AddEditTask = defineComponent({
  setup(props: { msg: string; isEditing: boolean; list: ItoDo[] }, { emit }) {
    // use Composition API here like in <script setup>
    const taskIndex = ref(0)
    const task = ref<ItoDo>({
      task: '',
      time: '',
      completed: false
    })
    const isVisible = ref(true)
    const twoDigit = (t: number | string) => ((typeof t === 'string' && t.length === 1) || (typeof t === "number" && t < 10)) ? '0' + t : t
      

    watch(taskIndex, (v) => {
      task.value = {...props.list[v], time: changeCustomToDate(props.list[v].time)}
    })
    onMounted(() => {
      task.value = {...props.list[0], time: changeCustomToDate(props.list[0].time)}
    })
    function changeDateToCustom(t: string){
      const d = new Date(t)
      return d.getDate() + '/' + (d.getMonth()+ 1) + '/' + d.getFullYear() + ' ' + twoDigit(d.getHours()) + ':' + twoDigit(d.getMinutes())
    }
    function changeCustomToDate(t: string){
      const [date, hours] = t.split(' ')
      const [day, month, year] = date.split('/')
      const [hour, minutes] = hours.split(':')
      return year + '-' + twoDigit(month) + '-' + twoDigit(day) + 'T' + twoDigit(hour) + ':' + twoDigit(minutes)
    }
    const onClick = (e: void) => {
      isVisible.value = false
      task.value.time = changeDateToCustom(task.value.time)
      emit('confirmed', task.value, taskIndex.value)
    }
    const onClose = () => {
      isVisible.value = false
      emit('close')
    }
    function setIndex(v: Event ) { taskIndex.value = parseInt((v.target as HTMLSelectElement).value) }
    const ti = computed(() => {
      if(props.isEditing) return (
        <select onChange={ setIndex }>
          { props.list.map((e, index: number) => <option value={index}>{index + 1}</option> )}
        </select>
      )
      return null
    })
    return () => {
      // render function or JSX
      return (
        <dialog style={{ display: isVisible.value ? 'flex': 'none', transform: 'translate(0, -50%)' }}>
          <span class="close" onClick={ onClose }/>
          <form class="flex-column" onSubmit={ (e) => onClick(e.preventDefault()) }>
            <h3>{ props.msg }</h3>
            { ti.value }
            <label for="task" class="required">Task:</label>
            <textarea rows="5" id="task" v-model={task.value.task} required/>
            <label for="time" class="required">Due to:</label>
            <input type="datetime-local" id="time" v-model={task.value.time} required/>
            <label>Completed: <input type="checkbox" v-model={task.value.completed}/></label>
            <button class="btn" style={{ width:'100%' }} type='submit'>Confirm</button>
          </form>
        </dialog>
      )
    }
  },
  // manual runtime props declaration is currently still needed.
  props: ['msg', 'isEditing', 'list'],
  emits: ['confirmed', 'close']
})
function addTask() {
  const confirmed = (task: ItoDo) => {
    todoList.value.push(task)
    closeModal()
  }
  dynamicCompon.value = <AddEditTask msg={'Add new task'} isEditing={false} onConfirmed={confirmed} onClose={closeModal}/>
}
function editTask() {
  const confirmed = (task: ItoDo, index: number) => {
    todoList.value[index] = task
    closeModal()
  }
  dynamicCompon.value = <AddEditTask msg={'Edit task'} isEditing={true} list={todoList.value} onConfirmed={confirmed} onClose={closeModal}/>
}
function toggleTask() {
  const selected = (index: number) => {
    toggle(index)
    closeModal()
  }
  dynamicCompon.value = <SelectTask msg={'Select task to toggle'} list={todoList.value} onSelected={selected} onClose={closeModal}/>
}
function removeTask() {
  const selected = (index: number) => {
    remove(index)
    closeModal()
  }
  dynamicCompon.value = <SelectTask msg={'Select tast to remove'} list={todoList.value} onSelected={selected} onClose={closeModal}/>
}
function toggleAll() { todoList.value.forEach(t => t.completed = true) }
function removeAll() { todoList.value = [] }
function toggle(index: number) { todoList.value[index].completed = !todoList.value[index].completed }
function remove(index: number) { todoList.value.splice(index, 1) }
function closeModal() { dynamicCompon.value = null }
</script>
<style scoped>
.task {
  display: grid;
  grid-template-columns: 20px auto 16ch 1fr 40px;
  column-gap: 2ch;
  align-items: center;
  &:nth-child(odd){
    background-color: azure;
  }
  .remove { grid-column: 5 / span 1; background-color: red; color: white; border: red; }
}
</style>