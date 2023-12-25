<template>
  <div>
    <!-- <div class="back" @click="backMenu">Назад</div> -->
    <div class="form_container">
      <div style="margin-bottom: 10px; font-size: 25px">Создание журнала СУГ</div>
      <form>
        <input placeholder="equipment_id" type="text" v-model="equipment_id" />
        <input placeholder="schedule_date" type="text" v-model="schedule_date" />
        <input placeholder="repair_type" type="text" v-model="repair_type" />
        <input placeholder="actual_date" type="text" v-model="actual_date" />
        <input placeholder="sug_detalis_id" type="text" v-model="sug_detalis_id" />
        <input placeholder="comment_" type="text" v-model="comment_" />
        <input placeholder="repair_mark" type="text" v-model="repair_mark" />
        <input placeholder="end_date" type="text" v-model="end_date" />
        <button @click.prevent="submit" class="btn_create">Создать</button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      equipment_id: '',
      schedule_date: '',
      repair_type: '',
      actual_date: '',
      sug_detalis_id: '',
      comment_: '',
      repair_mark: '',
      end_date: ''
    }
  },
  methods: {
    async submit() {
      let newSugJournal = {
        equipment_id: +this.equipment_id,
        schedule_date: this.schedule_date,
        repair_type: +this.repair_type,
        actual_date: this.actual_date,
        sug_detalis_id: +this.sug_detalis_id,
        comment_: this.comment_,
        repair_mark: this.repair_mark,
        end_date: this.end_date
      }
      console.log(newSugJournal)
      await axios
        .post('http://localhost:8080/api/create_sug_journal', newSugJournal)
        .then((res) => console.log(res))
    },
    backMenu() {}
  }
}
</script>

<style scoped>
form {
  padding: 15px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 500px;
  border: 1px solid rgba(0, 0, 0, 0.3);
  box-shadow: 5px 5px 5px rgba(0, 0, 0, 0.3);
  border-radius: 8px;
}

.form_container {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin-top: 5%;
}
input {
  /* width: 100%; */
  height: 30px;
  margin-bottom: 15px;
  font-size: 20px;
  border: 1px solid rgba(0, 0, 0, 0.5);
  border-radius: 5px;
  padding: 3px;
}
.btn_create {
  background: none;
  height: 25px;
  border: 1px solid rgba(0, 0, 0, 0.7);
  border-radius: 3px;
  width: 100%;
}
.btn_create:hover {
  background-color: rgba(0, 0, 0, 0.1);
}
.btn_create:active {
  background-color: rgba(0, 0, 0, 0.2);
}
.back {
  margin: 30px;
  border: 1px solid black;
  width: 80px;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 3px;
}
.back:hover {
  background-color: rgba(0, 0, 0, 0.1);
}
.back:active {
  background-color: rgba(0, 0, 0, 0.2);
}
</style>
