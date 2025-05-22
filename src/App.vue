<template>
  <div>
    <span>Lista oggetti da comprare</span>
    <Button label="Aggiungi" @click="addListObj"></Button>
    <div>
      <input v-model="enteredObjText">
    </div>
    <div>
      <ul>
        <li v-for="(oggetto, i) in objList" :key="i">
          <div v-if="editObjIndex !== i">
            {{ oggetto }}
            <Button label="cancella" @click="removeListObj(i)"></Button>
            <Button label="modifica" @click="editListObj(i)"></Button>
          </div>
          <div v-else>
            <input v-model="editObjText" />
            <Button label="Salva" @click="saveListObj(i)"></Button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Button from 'primevue/button';

export default {
  name: 'App',
  components: {
    HelloWorld,
    Button
  },
  data (){
    return {
      enteredObjText: '',
      objList: [],
      editObjText: null,
      editObjIndex: null,
    }
  },
  methods: {
    addListObj() {
      this.objList.push(this.enteredObjText);
    },
    removeListObj(index) {
      this.objList.splice(index, 1);
    },
    editListObj(index) {
      this.editObjIndex = index;
      this.editObjText = this.objList[index];
    },
    saveListObj(index) {
      const newList = [];
      this.objList.forEach((el, i) => {
        if (i === index) {
          newList.push(this.editObjText);
        } else {
          newList.push(el);
        }
      })

      this.objList = newList;
      this.editObjText = null;
      this.editObjIndex = null;
    },
  },
}
</script>