<template>
  <div class="left-panel">
    <resumeInput label="Профессия:" v-model="profession" />
    <resumeInput label="Город:" v-model="city" />
    <resumeInput label="Ссылка на фото:" v-model="photo" />
    <resumeInput label="ФИО:" v-model="FIO" />
    <resumeInput label="Номер телефона:" v-model="phone" regex="^\d{6,10}$" error_message="Неверный номер" />
    <resumeInput label="E-mail:" v-model="email" />
    <resumeInput label="День рождения:" v-model="BD" />
    <resumeSelect label="Образование" :options="['Среднее', 'Среднее специальное', 'Неоконченное высшее', 'Высшее']"
      v-model="education" />
    <resumeInput v-if="education != 'Среднее'" label="Учебное заведение:" v-model="education_place" />
    <resumeInput v-if="education != 'Среднее'" label="Факультет:" v-model="facultet" />
    <resumeInput v-if="education != 'Среднее'" label="Специализация:" v-model="specialization" />
    <resumeInput v-if="education != 'Среднее'" label="Год выпуска:" v-model="end_year" />
    <resumeInput label="Желаемый оклад:" v-model="salary" />
    <resumeInput label="Навыки:" v-model="skills" />
    <resumeInput label="О себе:" v-model="about_me" />
  </div>
  <div class="text-bg-dark">
    <div class="px-4 py-5">
      <div class="row align-items-stretch g-5 py-5 container" style="word-break:break-all">
      <h2 class="pb-2 border-bottom px-4">Профессия: {{ profession }}</h2>
        <img v-bind:src="photo" class="card card-cover overflow-hidden rounded-4 shadow-lg"
          style="width: 30%; color: black" id="photo" alt="Нет фото" />
        <div>
          <div>
            <h4>ФИО</h4>
            <p style="word-break: break-all">{{ FIO }}</p>
          </div>
          <div>
            <h4>ДР</h4>
            <p>{{ BD }}</p>
          </div>
          <div>
            <h4>Город</h4>
            <p style="word-break: break-all">{{ city }}</p>
          </div>
          <div>
            <h4>Email</h4>
            <p style="word-break: break-all">{{ email }}</p>
          </div>
          <div>
            <h4>Телефон</h4>
            <p>{{ phone }}</p>
          </div>
        </div>
        <div>
          <div>
            <h4>Образование</h4>
            <p style="word-break: break-all">{{ education }}</p>
          </div>
          <div id="edu_view" hidden="hidden">
            <div>
              <h4>Учебное заведение</h4>
              <p style="word-break: break-all">{{ education_place }}</p>
            </div>
            <div>
              <h4>Факультет</h4>
              <p style="word-break: break-all">{{ facultet }}</p>
            </div>
            <div>
              <h4>Специализация</h4>
              <p style="word-break: break-all">{{ specialization }}</p>
            </div>
            <div>
              <h4>Год окончания</h4>
              <p style="word-break: break-all">{{ end_year }}</p>
            </div>
          </div>
          <div>
            <h4>Навыки</h4>
            <p style="word-break: break-all">{{ skills }}</p>
          </div>
          <div>
            <h4>О себе</h4>
            <p style="word-break: break-all">{{ about_me }}</p>
          </div>
        </div>
      </div>
      <div>
        <h4>Желаемая ЗП</h4>
        <p>{{ salary }}</p>
      </div>
    </div>
  </div>
</template>

<script>
// import appResume from './components/appResume.vue'
import resumeInput from './components/resumeInput.vue'
import resumeSelect from './components/resumeSelect.vue'

export default {
  name: 'App',
  components: {
    // appResume,
    resumeSelect,
    resumeInput
  },
  data() {
    return {
      profession: "",
      photo: "",
      FIO: "",
      BD: "",
      city: "",
      email: "",
      phone: "",
      education: "",
      skills: "",
      about_me: "",
      salary: "",
      activeColor: "",
      activeColor1: "",
      activeColor2: "",
      education_place: "",
      facultet: "",
      specialization: "",
      end_year: "",
      feedback_1: "",
      feedback_2: "",
      feedback_3: "",
    }
  },
  watch: {
    education: function (neweducation) {
      //обработчик значений образования
      let zone1 = document.getElementById("education_input");
      let zone2 = document.getElementById("edu_view");
      if (
        neweducation == "Среднее специальное" ||
        neweducation == "Неоконченное высшее" ||
        neweducation == "Высшее"
      ) {
        zone1.removeAttribute("hidden"); //добавление или удаление атрибута hidden
        zone2.removeAttribute("hidden");
      } else {
        zone1.hidden = "hidden";
        zone2.hidden = "hidden";
      }
    },
    FIO: function (newFIO) {
      //обработчик фио
      this.FIO = newFIO;
      const regex = /[А-ЯA-Zа-яa-z -]/g;
      newFIO = newFIO.match(regex); //проверка на совпадение с регуляркой
      if (!newFIO) {
        this.feedback_3 =
          "неверный формат имени, допускаются только русские и английские буквы";
        // this.activeColor1 = "red";
      } else {
        this.feedback_3 = "";
        // this.activeColor1 = "black";
      }
    },
    email: function (newemail) {
      //обработчик почты
      this.email = newemail;
      const regex = /^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$/;
      newemail = newemail.match(regex); //проверка на совпадение с регуляркой
      if (!newemail) {
        this.feedback_1 =
          "неверный формат email, допускаются только английские буквы";
        //   this.activeColor = "red";
      } else {
        this.feedback_1 = "";
        //   this.activeColor = "black";
      }
    },
    phone: function (newphone) {
      //обработчик телефона
      this.phone = newphone;
      const regex = /^[0-9]{6,10}$/;
      newphone = newphone.match(regex); //проверка на совпадение с регуляркой
      if (!newphone) {
        this.feedback_2 =
          "неверный формат телефона, допускается 6-10 чисел, без служебных символов";
        // this.activeColor2 = "red";
      } else {
        this.feedback_2 = "";
        // this.activeColor2 = "black";
      }
    },
    photo: function (newphoto, oldphoto) {
      //обработчик смены фото
      if (!newphoto) {
        this.photo = oldphoto;
      } else {
        this.photo = newphoto;
      }
    },
  },
}
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
</style>
