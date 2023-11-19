<template>
  <form class="sign-up" @submit.prevent="checkForm">
    <!-- 1 -->
    <div v-show="step === 1" class="step">
      <div class="form-group">
        <!-- Фамилия -->
        <label for="lastName">Фамилия:</label>
        <input
          id="lastName"
          class="form-control"
          :class="$v.formFirst.lastName.$error ? 'is-invalid' : ''"
          v-model.trim="formFirst.lastName"
        />
        <p
          v-if="$v.formFirst.lastName.$dirty && !$v.formFirst.lastName.required"
          class="invalid-feedback"
        >
          Поле обязательно для заполнения
        </p>
      </div>
      <!-- Имя -->
      <div class="form-group">
        <label for="name">Имя:</label>
        <input id="name" class="form-control" v-model.trim="formFirst.name" />
        <p
          v-if="$v.formFirst.name.$dirty && !$v.formFirst.name.required"
          class="invalid-feedback"
        >
          Поле обязательно для заполнения
        </p>
      </div>
      <!-- Отчество -->
      <div class="form-group">
        <label for="sureName">Отчество:</label>
        <input
          id="sureName"
          class="form-control"
          v-model.trim="formFirst.sureName"
        />
      </div>
      <!-- Дата Рождения -->
      <div class="form-group">
        <label for="birthday">Дата Рождения:</label>
        <input
          id="birthday"
          class="form-control"
          v-model.trim="formFirst.birthday"
        />
        <p
          v-if="$v.formFirst.birthday.$dirty && !$v.formFirst.birthday.required"
          class="invalid-feedback"
        >
          Поле обязательно для заполнения
        </p>
      </div>
      <!-- Номер телефона -->
      <div class="form-group">
        <label for="numberPhone">Номер телефона:</label>
        <input
          id="numberPhone"
          class="form-control"
          v-model.trim="formFirst.numberPhone"
        />
      </div>
      <p
        v-if="
          $v.formFirst.numberPhone.$dirty && !$v.formFirst.numberPhone.required
        "
        class="invalid-feedback"
      >
        Поле обязательно для заполнения
      </p>

      <p
        v-if="
          $v.formFirst.numberPhone.$dirty && !$v.formFirst.numberPhone.numeric
        "
        class="invalid-feedback"
      >
        Неправильное поле ввода
      </p>
      <!-- Пол -->
      <div class="gender">
        <input
          type="radio"
          id="male"
          class="custom-checkbox"
          value="male"
          v-model="formFirst.gendere"
        />
        <label class="hzhz" for="male">Мужчина</label>
        <input
          type="radio"
          id="female"
          class="custom-checkbox"
          value="female"
          v-model="formFirst.gendere"
        />
        <label class="hz" for="female">Женщина</label>
      </div>
      <!-- Группа клиентов -->
      <div class="groupeClients">
        <label for="groupeClients">Группа</label>
        <select id="group" class="select-group">
          <option
            v-for="(group, index) in groupeClients"
            :value="groupeClients"
            :key="index"
          >
            {{ group.label }}
          </option>
        </select>
      </div>
      <!-- Врач -->
      <div class="doctor">
        <label for="doctors">Лечащий Врач</label>
        <select id="doctors" class="form-control" v-model.trim="chooseDoctor">
          <option
            v-for="(doctor, index) in doctors"
            :value="doctor.value"
            :key="index"
          >
            {{ doctor.label }}
          </option>
        </select>
      </div>

      <!-- sms -->
      <div class="Sms">
        <input
          type="checkbox"
          class="form-notification"
          id="notification"
          v-model="disagreeSendMessage"
        />
        <label class="pot" for="notification">Не отправлять СМС</label>
      </div>

      <button
        @click="nextStep"
        :disabled="disabledBtnFirst"
        type="submit"
        class="btn-next"
      >
        Далее
      </button>
    </div>

    <!-- 2 -->
    <transition name="slide-fade">
      name="slide-fade">
      <div v-show="step === 2" class="formSecond">
        <div class="form-group">
          <!-- Индекс -->
          <label for="index">Индекс:</label>
          <input
            id="index"
            class="form-control"
            v-model.trim="formSecond.index"
          />
        </div>
        <!-- Страна -->
        <div class="form-group">
          <label for="country">Страна:</label>
          <input
            id="country"
            class="form-control"
            v-model.trim="formSecond.country"
          />
        </div>
        <!-- Область -->
        <div class="form-group">
          <label for="region">Область:</label>
          <input
            id="region"
            class="form-control"
            v-model.trim="formSecond.region"
          />
        </div>
        <!-- Город -->
        <div class="form-group">
          <label for="city">Город:</label>
          <input
            id="city"
            class="form-control"
            v-model.trim="formSecond.city"
          />
          <p
            v-if="$v.formSecond.city.$dirty && !$v.formSecond.city.required"
            class="invalid-feedback"
          >
            Поле обязательно для заполнения
          </p>
        </div>
        <!-- Улица -->
        <div class="form-group">
          <label for="street">Улица:</label>
          <input
            id="street"
            class="form-control"
            v-model.trim="formSecond.street"
          />
        </div>

        <!-- Дом -->
        <div class="form-group">
          <label for="house">Дом:</label>
          <input
            id="house"
            class="form-control"
            v-model.trim="formSecond.house"
          />
        </div>
        <div class="buttons">
          <button @click="backStep" type="submit" class="btn-next">
            Назад
          </button>
          <button
            @click="nextStep"
            :disabled="disabledBtnSecond"
            type="submit"
            class="btn-next"
          >
            Далее
          </button>
        </div>
      </div>
    </transition>
    <!-- 3 -->
    <transition name="slide-fade">
      <div v-show="step === 3" class="step">
        <div class="doctor">
          <label for="doctors">Лечащий Врач</label>
          <select id="doctors" class="form-control" v-model.trim="chooseDoctor">
            <option
              v-for="(doctor, index) in doctors"
              :value="doctor.value"
              :key="index"
            >
              {{ doctor.label }}
            </option>
          </select>
        </div>

        <!-- Серия паспорта -->
        <div class="form-group">
          <label for="passportSeries">Серия:</label>
          <input
            id="passportSeries"
            class="form-control"
            v-model.trim="formThird.passportSeries"
          />
        </div>
        <!-- Номер -->
        <div class="form-group">
          <label for="numberPassport">Номер:</label>
          <input
            id="numberPassport"
            class="form-control"
            v-model.trim="formThird.numberPassport"
          />
        </div>
        <!-- Кем выдан -->
        <div class="form-group">
          <label for="issued">Кем выдан:</label>
          <input
            id="issued"
            class="form-control"
            v-model.trim="formThird.issued"
          />
        </div>
        <!-- Дата выдачи -->
        <div class="form-group">
          <label for="dateIssue">Дата выдачи:</label>
          <input
            id="dateIssue"
            class="form-control"
            v-model.trim="formThird.dateIssue"
          />
        </div>
        <p
          v-if="
            $v.formThird.dateIssue.$dirty && !$v.formThird.dateIssue.required
          "
          class="invalid-feedback"
        >
          Поле обязательно для заполнения
        </p>
        <div class="buttons">
          <button @click="backStep" type="submit" class="btn-next">
            Назад
          </button>
          <button
            @click="endRegistration"
            :disabled="disabledBtnThird"
            type="submit"
            class="btn-next"
          >
            Готово
          </button>
        </div>
      </div>
    </transition>
  </form>
</template>

<script>
import { validationMixin } from "vuelidate";
import {
  required,
  numeric,
  minLength,
  maxLength,
} from "vuelidate/lib/validators";

export default {
  mixins: [validationMixin],
  data() {
    return {
      step: 1,
      formFirst: {
        lastName: "",
        name: "",
        sureName: "",
        birthday: "",
        numberPhone: "",
        gendere: "male",
        chooseDoctor: ["Иванов"],
      },
      formSecond: {
        index: "",
        country: "",
        region: "",
        city: "",
        street: "",
        house: "",
      },
      formThird: {
        passportSeries: "",
        numberPassport: "",
        issue: "",
        dateIssue: "",
      },
      disagreeSendMessage: false,
      groupeClients: [
        {
          label: "VIP",
          value: "VIP",
        },
        {
          label: "Проблемные",
          value: "problems",
        },
        {
          label: "ОМС",
          value: "OMS",
        },
      ],
      doctors: [
        { label: "Иванов", value: "Ivanov" },
        { label: "Захаров", value: "Zaharov" },
        { label: "Чернышева", value: "Chernisheva" },
      ],
    };
  },
  validations: {
    formFirst: {
      lastName: { required },
      name: { required },
      sureName: { required },
      birthday: { required },
      numberPhone: {
        required,
        numeric,
        minLength: minLength(11),
        maxLength: maxLength(11),
      },
    },
    formSecond: {
      city: { required },
    },
    formThird: {
      dateIssue: { required },
    },
  },
  computed: {
    disabledBtnFirst() {
      return (
        this.$v.formFirst.lastName.$invalid ||
        this.$v.formFirst.name.$invalid ||
        this.$v.formFirst.sureName.$invalid ||
        this.$v.formFirst.birthday.$invalid ||
        this.$v.formFirst.numberPhone.$invalid
      );
    },
    disabledBtnSecond() {
      return this.$v.formSecond.city.$invalid;
    },
    disabledBtnThird() {
      return this.$v.formThird.dateIssue.$invalid;
    },
  },
  methods: {
    nextStep() {
      this.step++;
    },
    backStep() {
      this.step--;
    },
    endRegistration() {
      alert("Успешно ");
    },
    checkForm() {
      this.$v.formFirst.$touch();
      if (!this.$v.formFirst.$error) {
        console.log("Валидация прошла успешно");
      }
    },
  },
};
</script>

<style>
html {
  background-color: #000000cf;
}
.sign-up {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 300px;
}
.form-group {
  display: flex;
  flex-direction: column;
  padding-top: 10px;
}

.gender {
  margin: 10px;
}
label {
  font-weight: bold;
  color: #ffd3d3;
  margin-bottom: 5px;
}
input {
  padding: 10px;
  padding-right: 70px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
}
input:hover {
  border-color: #007bff;
}
input:focus {
  outline: none;
  box-shadow: 0 0 5px #007bff;
}

/* .groupeClients {
} */

.select-group {
  margin-left: 10px;
}

.doctor {
  display: flex;
  flex-direction: column;
  padding-top: 10px;
}

.Sms {
  margin-top: 10px;
}

.btn-next {
  margin-top: 10px;
  background-color: #007bff;
  color: #ffffff;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  text-align: center;
  transition: background-color 0.3s ease;
}

button:disabled {
  background-color: lightgray;
  color: gray;
}

.buttons button {
  margin: 15px 5px 0px 0px;
}

.invalid-feedback {
  display: block;
  color: #dc3545;
  font-size: 14px;
  margin-top: 5px;
}

.form-control {
  width: 200px;
}

.slide-fade-enter-active {
  transition: all 0.3s ease;
}
.slide-fade-enter,
.slide-fade-leave-to {
  transform: translateX(10px);
  opacity: 0;
}
</style>
