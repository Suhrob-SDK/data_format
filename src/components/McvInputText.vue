<template>
  <div class="app">
    <div class="data">  
      <center>     
        <table border="0">
          <tr>            
            <td>
              <input class="input" type="text" v-model="telAgent" placeholder="Тел Агентство">
            </td>
            <td>
              <input class="input" type="text" v-model="telPass" placeholder="Тел Пассажира">
            </td>
            <td>
              <input class="input" type="text" v-model="email" placeholder="Эл.почта">
            </td> 
            <td>
              <my-button @click="createElement">
                Добавить
              </my-button>                
            </td>           
          </tr>
        </table>               
          <table border="0">  
            <tbody>    
              <div v-for="(item, index) in items" :key="item.id">         
                <tr> 
                  <td>
                    {{ index+1 }}
                  </td>                 
                  <td>
                    <input class="input " type="text" v-model="item.surname" placeholder="Фамилия">
                  </td>
                  <td>
                    <input class="input " type="text" v-model="item.name" placeholder="Имя">
                  </td>
                  <td>
                    <input class="input " type="text" v-model="item.birthday" placeholder="Дата рождение">
                  </td>
                  <td>
                    <label v-for="gend in genders" :key="gend.id">
                      <input type="radio" :value="gend" v-model=" item.gender" /><br>
                      <span>{{ gend.name }}</span>
                    </label> 
                  </td>
                  <td>
                    <select class="select " v-model="item.citizenship">
                      <option v-for="c in citizenships" :value="c" v-bind:key="c.id">{{ c.name }} </option>
                    </select>
                  </td>
                  <td>
                    <input class="input " type="text" v-model="item.passportSeries" placeholder="Серия пасспорт">
                  </td>
                  <td>
                    <input class="input " type="text" v-model="item.passportExpirationDate" placeholder="Срок пасспорт">
                  </td>              
                </tr>
              </div>
            </tbody>
          </table>        
      </center>
    </div>
    <div class="data" >
      <h2>
        9А# {{ telAgent }} <br>
        9M# {{ telPass }} <br>
        9П1E# {{ email }} <br>
      </h2>    
      <div v-for="(item) in items" :key="item.id">        
          <h2>          
           -{{ item.surname }} {{ item.name }} {{ item.birthday }}+{{ gender.code }}/{{ citizenship.code }}/{{ citizenship.pass }}{{ item.passportSeries }}/{{ item.passportExpirationDate }}        
          </h2>         
      </div>
    </div>
  </div>
</template>

<script>
import MyButton from '@/components/MyButton.vue';

export default {
	components: { MyButton },
  data (){
    const citizenships = [
        {id: 1, code: "TJ", name: "Таджикистан", pass: "НП"},
        {id: 2, code: "RU", name: "Россия", pass: "УДЛ"},
        {id: 3, code: "UZ", name: "Узбекистан", pass: "УЗНП"},
    ];
    const genders = [
        {id: 1, name: 'Мужчина', code: "М" }, 
        {id: 2, name: 'Женшина', code: "Ж" }
    ];
    return {
      items: [
        { 
         id: '', 
         surname: '' ,
         name: '' ,
         birthday: '' ,     
         passportSeries: '' ,
         passportExpirationDate: '',            
        },  
      ],
      citizenships,
      citizenship: citizenships[0] ,         
      genders ,
      gender: genders[0], 
      telAgent: '', 
      telPass: '', 
      email: '' ,
      
      formModel: {
         id: '', 
         surname: '' ,
         name: '' ,
         birthday: '' ,     
         passportSeries: '' ,
         passportExpirationDate: '', 
         gender: '',
         citizenship: '',
      }
    }  
  },
  methods: {
    createElement (){
      this.items.push({ ...this.formModel }),  
      this.formModel.id = '' 
      this.formModel.surname = ''
      this.formModel.name = ''
      this.formModel.birthday = ''     
      this.formModel.passportSeries = ''
      this.formModel.passportExpirationDate = '' 
      this.formModel.gender = ''
      this.formModel.citizenship = ''              
    },
  },
  mounted() {
    if(localStorage.telAgent) this.telAgent = localStorage.telAgent;
    if(localStorage.telPass) this.telPass = localStorage.telPass;
    if(localStorage.email) this.email = localStorage.email;
  },
  watch: {
    telAgent(newName) {
      localStorage.telAgent = newName;
    },
    telPass(newName) {
      localStorage.telPass = newName;
    },
    email(newName) {
      localStorage.email = newName;
    },
  },  
  
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 5px;
}

.data {
  padding: 5px;
  border: 2px solid teal;
  margin-top: 10px;
}

.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 5px;   
  font-size:25px;
}

.select {  
  border: 1px solid teal;
  padding: 10px 15px;  
  font-size:25px;  
}

th, td {
  padding: 5px;
}

</style>