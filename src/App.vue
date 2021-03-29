<template>
  <div class="container mt-3">
    <form v-if="!formSuccess">
      <b-progress :max="info.length" :value="fieldsDone"></b-progress>
      <div>
        <app-field
          v-for="(field, i) in info"
          :key="i"
          :value="field.value"
          :name="field.name"
          :valid="field.valid"
          @updated="onInput(i, $event)"
        ></app-field>
      </div>
      <button class="btn btn-primary" :disabled="'disabled' ? !formReady : ''" type="button" @click="popupIsVisible = true">
        Send Data
      </button>
    </form>
    <transition name="down" appear>
      <Popup v-if="popupIsVisible" @hide-popup="popupIsVisible = false">
        <table class="table table-bordered">
          <tr v-for="item in info" :key="item.name">
            <td>{{ item.name }}</td>
            <td>{{ item.value }}</td>
          </tr>
        </table>
        <div class="buttons">
          <button class="btn btn-success" @click="showResult">Ok</button>
          <button class="btn btn-primary" @click="popupIsVisible = false">Cancel</button>
        </div>
      </Popup>
    </transition>
    <transition name="fade" appear>
      <Overlay v-if="popupIsVisible" @click.native="popupIsVisible = false"/>
    </transition>
    <h3 v-if="formSuccess">All done...</h3>
  </div>
</template>
<script>
import AppField from '@/components/Field.vue'
import {BProgress} from 'bootstrap-vue'
import Popup from "./components/Popup";
import Overlay from "./components/Overlay";

export default {
  components: {
    Overlay,
    Popup,
    AppField,
    BProgress
  },
  data: () => ({
    popupIsVisible: false,
    formSuccess: false,
    info: [
      {
        name: 'Name',
        value: '',
        pattern: /^[a-zA-Z ]{2,30}$/
      },
      {
        name: 'Phone',
        value: '',
        pattern: /^[0-9]{7,14}$/
      },
      {
        name: 'Email',
        value: '',
        pattern: /.+/
      },
      {
        name: 'Some Field 1',
        value: '',
        pattern: /.+/
      },
      {
        name: 'Some Field 2',
        value: '',
        pattern: /.+/
      }
    ]
  }),
  computed: {
    fieldsDone () {
      return this.info.reduce((total, field) => {
        return total + (field.valid ? 1 : 0);
      }, 0);
    },
    formReady () {
      return this.fieldsDone === this.info.length;
    }
  },
  methods: {
    onInput (i, value) {
      let field = this.info[i];
      field.value = value.trim();
      field.valid = field.pattern.test(field.value);
    },
    closePopup () {
      this.popupIsVisible = false
    },
    showResult () {
      this.closePopup()
      this.formSuccess = true
    }
  },
  created () {
    return this.info.forEach(field => {
      this.$set(field, 'valid', field.pattern.test(field.value));
    });
  }
}
</script>
<style>
@keyframes fadeIn{
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
.fade-enter-active {
  animation: fadeIn .5s ease;
}
.fade-leave-active {
  animation: fadeIn .2s ease reverse;
}
@keyframes fadeInDown {
  0% {
    opacity: 0;
    transform: translateY(-20rem);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
.down-enter-active {
  animation: fadeInDown .5s ease;
}
.down-leave-active {
  animation: fadeInDown .2s ease reverse;
}
</style>
