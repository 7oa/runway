<template>
  <div class="address-book">
    <div
      class="address-book__current"
      :class="editAddressList && 'address-book__current_edit'"
    >
      <div class="address-book__current-title">Текущий адрес доставки</div>
      <div v-if="!editAddressList" class="address-book__change-button">
        <button
          class="button-link button-link_gray"
          @click.prevent="editAddressList = true"
        >
          изменить
        </button>
      </div>
      <AddressItem
        v-for="address of addressList"
        :key="address.id"
        :address="address"
        :editMode="editAddressList"
        @remove-address="removeAddress"
        @set-active-address="setActiveAddress"
      />
    </div>
    <div v-if="!addAdressShow" class="address-book__add-button">
      <button class="button button_gray" @click.prevent="addAdressShow = true">
        Добавить еще один адрес
      </button>
    </div>
    <div class="address-book__add" v-else>
      <div class="address-book__add-title">Добавить адрес</div>
      <div class="add-address-form">
        <div class="add-address-form__line">
          <div class="input-wrapper input-wrapper_third">
            <input
              type="string"
              placeholder="Индекс"
              class="input input_full input_sm"
              v-model="index"
              v-mask="'### ###'"
            />
          </div>
          <div class="input-wrapper input-wrapper_third">
            <div class="select select_full">
              <select
                type="text"
                placeholder="Страна"
                class="select__select select__select_sm"
                v-model="country"
              >
                <option value="" disabled selected>Страна</option>
                <option>Россия</option>
                <option>США</option>
                <option>Индия</option>
                <option>Япония</option>
              </select>
            </div>
          </div>
          <div class="input-wrapper input-wrapper_third">
            <div class="select select_full">
              <select
                type="text"
                placeholder="Город"
                class="select__select select__select_sm"
                v-model="city"
              >
                <option value="" disabled selected>Город</option>
                <option>Москва</option>
                <option>Лондон</option>
                <option>Таллин</option>
                <option>Сидней</option>
              </select>
            </div>
          </div>
        </div>
        <div class="add-address-form__line">
          <div class="input-wrapper input-wrapper_full">
            <input
              type="text"
              placeholder="Адрес"
              class="input input_full input_sm"
              v-model="inputAddress"
            />
          </div>
        </div>
      </div>
      <div class="add-address-form__button">
        <button class="button button_orange" @click.prevent="addAdress">
          Добавить адрес
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import AddressItem from "./AddressItem.vue";
import { mask } from "vue-the-mask";

export default {
  directives: { mask },
  data() {
    return {
      index: "",
      country: "",
      city: "",
      inputAddress: "",
      editAddressList: false,
      addAdressShow: false,
      addressList: [
        {
          id: 1,
          value: "432 071 Россия, г. Троицк, ул. Ленина д.34. кв.54",
          active: true
        },
        {
          id: 2,
          value:
            "445 086 Россия, г. Керчь, ул. Первого Интернационала д.14. кв.6",
          active: false
        }
      ]
    };
  },
  components: {
    AddressItem
  },
  methods: {
    addAdress() {
      if (this.inputAddress.trim()) {
        const newAddress = {
          id: Date.now(),
          value: `${this.index} ${this.country}, ${this.city}, ${this.inputAddress}`,
          active: false
        };

        this.addressList.push(newAddress);
        this.index = "";
        this.country = "";
        this.city = "";
        this.inputAddress = "";
      }
    },
    removeAddress(id) {
      this.addressList = this.addressList.filter(item => item.id != id);
    },
    setActiveAddress(id) {
      this.addressList = this.addressList.map(el => {
        if (el.id == id) el.active = true;
        else el.active = false;
        return el;
      });
    }
  }
};
</script>
