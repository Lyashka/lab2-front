<template>
  <MainHeaderVue></MainHeaderVue>
  <main>
    <SugForm v-show="visibleSugForm"></SugForm>
    <ComForm v-show="visibleComForm"></ComForm>
    <div class="container_sug_com">
      <div style="margin-right: 50px; text-align: center" v-show="visible_btn">
        <button @click="openSugForm" class="btn">Add sug journal</button>
        <div class="lable_rep">Создать отчет за месяц для журнала СУГ</div>
        <input placeholder="Введите дату" type="text" v-model="sugDate" />
        <button @click="createReportSug" class="btn_rep">Сформировать</button>
      </div>

      <div style="text-align: center" v-show="visible_btn">
        <button @click="openComForm" class="btn">Add component journal</button>
        <div class="lable_rep">Создать отчет за месяц для журнала Компонент</div>
        <input placeholder="Введите дату" type="text" v-model="comDate" />
        <button @click="createReportCom" class="btn_rep">Сформировать</button>
      </div>
    </div>
  </main>
</template>

<script>
import MainHeaderVue from '../components/MainHeader.vue'
import SugForm from '../components/SugForm.vue'
import ComForm from '../components/ComForm.vue'

import axios from 'axios'
export default {
  components: {
    MainHeaderVue,
    SugForm,
    ComForm
  },
  data() {
    return {
      visibleSugForm: false,
      visibleComForm: false,
      visible_btn: true,

      sugDate: '',
      comDate: ''
    }
  },
  methods: {
    openSugForm() {
      ;(this.visibleSugForm = true), (this.visibleComForm = false), (this.visible_btn = false)
    },
    openComForm() {
      ;(this.visibleSugForm = false), (this.visibleComForm = true), (this.visible_btn = false)
    },

    async createReportSug() {
      let newSugRep = {
        id_mounth: this.sugDate
      }
      await axios
        .post('http://localhost:8080/api/create_sug_report', newSugRep)
        .then((res) => console.log(res))
    },

    async createReportCom() {
      let newComRep = {
        id_mounth: this.comDate
      }
      await axios
        .post('http://localhost:8080/api/create_com_report', newComRep)
        .then((res) => console.log(res))
    }
  }
}
</script>

<style scoped>
.container_sug_com {
  position: absolute;
  top: 50%;
  margin-left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
}
.btn {
  border-radius: 8px;
  font-size: xx-large;
  width: 500px;
  height: 300px;
  margin-bottom: 50px;
  background-color: aliceblue;
}
.btn:hover {
  background-color: rgba(0, 0, 0, 0.1);
}
.btn:active {
  background-color: rgba(0, 0, 0, 0.2);
}
input {
  height: 30px;
  width: 200px;
  margin-right: 10px;
  font-size: 20px;
}
.btn_rep {
  padding: 5px;
  height: 30px;
  background: none;
  border: none;
  border: 1px solid rgba(0, 0, 0, 0.6);
  border-radius: 4px;
}
.btn_rep:hover {
  background-color: rgba(0, 0, 0, 0.1);
}
.btn_rep:active {
  background-color: rgba(0, 0, 0, 0.3);
}
.lable_rep {
  font-size: 18px;
  margin-bottom: 10px;
}
</style>
