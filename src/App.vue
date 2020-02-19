<template>
  <div id="app">
    <h1 class="main-title">Мои настройки</h1>
    <form action="">
      <h2 class="subtitle">Личные данные</h2>
      <div class="group">
        <Field v-for="field of fields.private" :key="field.id" :field="field" />
      </div>

      <h2 class="subtitle">Контактные данны</h2>
      <div class="group">
        <Field
          v-for="field of fields.contacts"
          :key="field.id"
          :field="field"
        />
      </div>

      <h2 class="subtitle">Адресная книга</h2>
      <div class="group">
        <AdressList />
      </div>

      <h2 class="subtitle">Подписки и уведомления</h2>
      <div class="group">
        <SubscriptionItem
          v-for="subscription of fields.subscriptions"
          :key="subscription.id"
          :subscription="subscription"
        />
      </div>
    </form>
  </div>
</template>

<script>
import Field from "./components/Field.vue";
import AdressList from "./components/AdressList.vue";
import SubscriptionItem from "./components/SubscriptionItem.vue";

export default {
  name: "App",
  data: function() {
    return {
      fields: {
        private: [
          { id: 1, label: "Имя", value: "", type: "text" },
          { id: 2, label: "Фамилия", value: "", type: "text" },
          { id: 3, label: "Отчество", value: "", type: "text" },
          {
            id: 4,
            label: "Дата рождения",
            value: "",
            type: "text",
            placeholder: "дд.мм.гггг",
            pattern: "##.##.####"
          }
        ],
        contacts: [
          {
            id: 5,
            label: "+7 (___) -__ - __",
            value: "",
            type: "tel",
            pattern: "+7 (###) -## - ##"
          },
          { id: 6, label: "E-mail", value: "", type: "email" },
          {
            id: 7,
            label: "Пароль [********]",
            value: "",
            type: "password"
          }
        ],
        subscriptions: [
          {
            id: 8,
            value: "Оповещать меня о текущих акциях по e-mail",
            active: true
          },
          {
            id: 9,
            value: "Оповещать меня о текущих акциях по Sms",
            active: true
          }
        ]
      }
    };
  },
  components: {
    Field,
    AdressList,
    SubscriptionItem
  }
};
</script>
