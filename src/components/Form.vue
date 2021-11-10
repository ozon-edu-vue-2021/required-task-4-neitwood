<template>
  <div class="form">
    <h2>Личные данные</h2>
    <div class="fio">
      <Input caption="Фамилия" v-model="surname" />
      <Input caption="Имя" v-model="name" />
      <Input caption="Отчество" v-model="patronymic" />
    </div>
    <div class="birthday">
      <Input
        caption="Дата рождения"
        placeholder="дд.мм.гггг"
        v-model="birthday"
      />
    </div>
    <div class="email">
      <Input caption="E-mail" v-model="email" />
    </div>
    <h2>Пол</h2>
    <div class="gender">
      <Radio :id="'male'" label="Мужской" name="gender" :value="gender" @change="changeGender" />
      <Radio :id="'female'" label="Женский" name="gender" :value="gender" @change="changeGender" />
    </div>
    <h2>Паспортные данные</h2>
    <div class="citizenship">
      <Select caption="Гражданство" :options="citizenships" v-model="citizenship" />
    </div>
    <div class="passport" v-if="isRussian">
      <Input caption="Серия паспорта" />
      <Input caption="Номер паспорта" />
      <Input caption="Дата выдачи" placeholder="дд.мм.гг" />
    </div>
    <h2>Меняли ли фамилию или имя?</h2>
    <div class="is-change-fio">
      <Radio :id="'no'" label="Нет" name="is-change-fio" :value="isChangeFio" @change="changeFio" />
      <Radio :id="'yes'" label="Да" name="is-change-fio" :value="isChangeFio" @change="changeFio" />
    </div>
    <div class="prev-names" v-if="isChangeFio === 'Да'">
      <Input caption="Предыдущая фамилия" v-model="prevName" />
      <Input caption="Предыдущее имя" v-model="prevSurname"/>
    </div>
    <div class="names">
      <Input caption="Фамилия на латинице" v-if="!isRussian"/>
      <Input caption="Имя на латинице" v-if="!isRussian"/>
    </div>
    <div class="other">
      <Input caption="Номер паспорта" v-if="!isRussian"/>
      <Select caption="Страна выдачи" :options="countries" v-model="country" v-if="!isRussian"/>
      <Select caption="Тип паспорта" :options="passportTypes" v-model="passportType" v-if="!isRussian"/>
    </div>
    <div class="send">
      <button @click="sendJson">Отправить</button>
    </div>
  </div>
</template>

<script>
import Input from "./Input";
import Select from "./Select";
import Radio from "./Radio";
import citizenships from "../assets/data/citizenships.json";
import passportTypes from "../assets/data/passport-types.json";

export default {
  components: {
    Input,
    Select,
    Radio,
  },
  data() {
    return {
      countries: [],
      country: "Russia",
      citizenships: [],
      citizenship: "Russian",
      passportTypes: [],
      passportType: "Национальный паспорт",
      surname: "",
      name: "",
      patronymic: "",
      birthday: "",
      email: "",
      gender: "Мужской",
      isChangeFio: "Нет",
      prevName: "",
      prevSurname: "",
    };
  },
  mounted() {
    this.citizenships = citizenships.map((el) => {
      return { id: el.id, text: el.language, value: el.language }
    });
    this.countries = citizenships.map((el) => {
      return { id: el.id, text: el.nationality, value: el.nationality }
    });
    this.passportTypes = passportTypes.map((el) => {
      return { id: el.id, text: el.type, value: el.type }
    });
  },
  methods: {
    changeGender: function(newValue) {
      this.gender = newValue;
    },
    changeFio: function(newValue) {
      this.isChangeFio = newValue;
    },
    sendJson() {
      console.log(this.$data);
    }
  },
  computed: {
    isRussian: function () {
      if( this.citizenship === "Russian") return true;
      return false;
    }
  }
};
</script>

<style scoped>
.form {
}
.fio,
.birthday,
.email,
.gender,
.is-change-fio,
.citizenship,
.passport,
.names,
.prev-names,
.other {
  display: flex;
  flex-direction: row;
}
.send{
  margin-top: 20px;
}
</style>
