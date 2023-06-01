<template>

<div class="wrapper">
<div class="wrapper-content">

<section>

<div class="container"> 
  
<NewMessege v-if="NewMessege" :NewMessege="NewMessege"/> 
<NewImr v-if="NewImr" :NewImr="NewImr"/>

<div class="new-note">

<label>Title</label> 
<input type="text" v-model="note.title"> 
<label>Importance</label>
<select v-model="note.impr">
      <option v-for="important in importants" :key="important.index">{{ important }}</option>
   </select>
<label>Description</label> 
<textarea v-model="note.descr"></textarea>
      
<button class="btn btnPrimary" @click="AddNote">New note</button>

</div>

<div class="note-header">
<h1>{{ title }}</h1>

<search :value="search" 
placeholder="Find the note"
@search=" search = $event"/>

<div class="icons">
  <svg :class="{ active: grid }" @click="grid = true" style="cursor: pointer;" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
  <svg :class="{ active: !grid }" @click="grid = false" style="cursor: pointer;" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>

</div>
</div>

<notes :notes="notesFilter" :grid="grid" @remove="removeNote"/>

</div>

</section>

</div>

</div>

</template>

<script>

import NewMessege from '@/components/NewMessege.vue'
import NewImr from '@/components/NewImpr.vue'
import notes from '@/components/ZametkiNovye.vue'
import Search from './components/SearchNote.vue'

export default {
  name: 'App',
  components: {
    NewMessege,
    NewImr,
    notes,
    Search
  },
  data () {
    return {
    title: 'Notes App',
    NewMessege: null,
    NewImr: null,
    grid: true,
    search: '',
    importants: ['Important', 'Normal', 'No matter'],
    note: {
      title:'',
      descr:'',
      impr: ''
    },
    notes: [
      {
        title: 'First note',
        descr: 'Description for first note',
        impr: 'Important',
        date: new Date(Date.now()).toLocaleString()
      },
      {
        title: 'Second note',
        descr: 'Description for second note',
        impr: 'Normal',
        date: new Date(Date.now()).toLocaleString()
      },
      {
        title: 'Third note',
        descr: 'Description for third note',
        impr: 'No matter',
        date: new Date(Date.now()).toLocaleString()
      },
    ]
  }
  },
  computed: {
    notesFilter () {
      let array = this.notes
      let search = this.search

      if (!search) return array //Чтобы поиск не искал пустую строку, т.е. если search равно false
      search = search.trim().toLowerCase() //Избовляем то, что будем искать от пробелов (trim()) и приводим это к нижнему регистру (toLowerCase())

      array = array.filter (function (item) {if (item.title.toLowerCase().indexOf(search) !== -1) 
      return item})

      return array
    }
  },
  methods: {
    AddNote () {
      let {title, descr, impr} = this.note

      if (title === '') {

        this.NewMessege = 'Wrong note'
        return false

      }
      if (impr === '') {

      this.NewImr = 'Choose the importance of note'
      return false

      }
      this.notes.push({
        title,
        descr,
        impr,
        date: new Date(Date.now()).toLocaleString()
      })
      this.NewMessege = null
      this.NewImr = null
      this.note.title = ''
      this.note.descr = ''
      this.note.impr = ''
    },
    removeNote (index) {
      this.notes.splice(index, 1)
    },
    СhangeNote () {
        let {title} = this.note

        this.notes.splice({
          title
        })
        this.note.title = ''
        
    }
  }
}
</script>

<style>

.new-note {
  text-align: center;
}

</style>

//ДЗ видос номер 34