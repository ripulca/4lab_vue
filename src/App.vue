<template>
  <div style="display:flex;flex-direction:row;">
    <div class="container px-4 py-5" style="width: 50%;">
      <resumeInput label="Профессия:" v-model="profession" />
      <resumeInput label="Город:" v-model="city" />
      <resumeInput label="Ссылка на фото:" v-model="photo" />
      <resumeInput label="ФИО:" v-model="FIO" regex="[А-ЯA-Zа-яa-z]"
        error_message="неверный формат имени, допускаются только русские и английские буквы" />
      <resumeInput type_inp="phone" label="Номер телефона:" v-model="phone" regex="^[0-9]{6,11}$"
        error_message="неверный формат телефона, допускается 6-10 чисел, без служебных символов" />
      <resumeInput type_inp="email" label="E-mail:" v-model="email" regex="^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z]+$"
        error_message="неверный формат email, допускаются только английские буквы" />
      <resumeInput type_inp="date" label="День рождения:" v-model="BD" />
      <resumeSelect label="Образование" :options="['Среднее', 'Среднее специальное', 'Неоконченное высшее', 'Высшее']"
        v-model="education" />
      <div v-if="education != 'Среднее'&&education!=''">
        <resumeInput label="Учебное заведение:" v-model="education_place" />
        <resumeInput label="Факультет:" v-model="facultet" />
        <resumeInput label="Специализация:" v-model="specialization" />
        <resumeInput label="Год выпуска:" v-model="end_year" />
      </div>
      <resumeInput label="Желаемый оклад:" v-model="salary" />
      <resumeInput label="Навыки:" v-model="skills" />
      <resumeInput label="О себе:" v-model="about_me" />
    </div>
    <div class="text-bg-dark" style="width: 50%;">
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
  </div>
</template>

<script>
import resumeInput from './components/resumeInput.vue'
import resumeSelect from './components/resumeSelect.vue'

export default {
  name: 'App',
  components: {
    resumeSelect,
    resumeInput,
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
      education_place: "",
      facultet: "",
      specialization: "",
      end_year: "",
    }
  },
}
</script>
