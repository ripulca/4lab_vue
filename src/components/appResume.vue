<template>
  <div id="form">
    <div class="px-4 py-3">
      <h2>Мое офигенное резюме</h2>
      <br />
      <div>
        <p>Ссылка на фото</p>
        <input type="text" id="photo" v-model="photo" />
      </div>
      <br />
      <div>
        <p>Введите ФИО</p>
        <input :style="{ color: activeColor1 }" type="text" id="FIO" v-model="FIO" />
        <p id="feedback_3">{{ feedback_3 }}</p>
      </div>
      <br />
      <div>
        <p>Введите ДР</p>
        <input type="date" id="BD" v-model="BD" />
      </div>
      <br />
      <div>
        <p>Введите город</p>
        <input type="text" id="city" v-model="city" />
      </div>
      <br />
      <div>
        <p>Введите email</p>
        <input :style="{ color: activeColor }" type="text" id="email" v-model.lazy="email" />
        <p id="feedback_1">{{ feedback_1 }}</p>
      </div>
      <br />
      <div>
        <p>Введите телефон</p>
        <input :style="{ color: activeColor2 }" type="tel" id="phone" v-model.lazy="phone" />
        <p id="feedback_2">{{ feedback_2 }}</p>
      </div>
      <br />
      <div>
        <p>Выберите образование</p>
        <select id="education" v-model="education">
          <option value="">Не выбрано</option>
          <option value="Среднее">Среднее</option>
          <option value="Среднее специальное">Среднее специальное</option>
          <option value="Неоконченное высшее">Неоконченное высшее</option>
          <option value="Высшее">Высшее</option>
        </select>
      </div>
      <br />
      <div id="education_input" hidden="hidden">
        <div>
          <p>Введите учебное заведение</p>
          <input type="text" id="education_place" v-model="education_place" />
          <br />
        </div>
        <div>
          <p>Введите факультет</p>
          <input type="text" v-model="facultet" />
          <br />
        </div>
        <div>
          <p>Введите специализацию</p>
          <input type="text" v-model="specialization" />
          <br />
        </div>
        <div>
          <p>Введите год окончания</p>
          <input type="number" v-model="end_year" />
          <br />
        </div>
      </div>
      <div>
        <p>Введите свои навыки</p>
        <input type="text" id="skills" v-model="skills" />
      </div>
      <br />
      <div>
        <p>Введите информацию о себе</p>
        <input type="text" id="about_me" v-model="about_me" />
      </div>
      <br />
      <div>
        <p>Введите желаемую ЗП</p>
        <input type="number" id="salary" v-model.number="salary" />
      </div>
    </div>
    <div class="text-bg-dark">
      <div class="px-4 py-5">
        <h2 class="pb-2 border-bottom px-4">Профессия</h2>
        <div class="row align-items-stretch g-5 py-5 container">
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
  </div>
</template>
<script>
export default {
  name: "appResume",
  data() {
    return {
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
};
</script>
