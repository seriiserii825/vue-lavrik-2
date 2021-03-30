<template>
  <div class="form-group">
    <label>{{ name }}</label>
    <transition v-if="activated" name="icon" mode="out-in" appear appear-active-class="icon-appear-active">
      <fa-icon :name="icon" :key="icon" :class="iconClasses"></fa-icon>
    </transition>
    <input type="text"
           class="form-control"
           :value="value"
           @input="onInput"
    >
  </div>
</template>
<script>
import FaIcon from 'vue-awesome/components/Icon'
import 'vue-awesome/icons/check-circle'
import 'vue-awesome/icons/exclamation-circle'

export default {
  components: {
    FaIcon
  },
  props: ['name', 'value', 'valid'],
  data () {
    return {
      activated: this.value !== ''
    }
  },
  computed: {
    icon () {
      return this.valid ? 'check-circle' : 'exclamation-circle';
    },
    iconClasses () {
      return this.valid ? 'text-success' : 'text-danger';
    }
  },
  methods: {
    onInput (e) {
      this.activated = true;
      this.$emit('updated', e.target.value);
    }
  }
}
</script>
<style>
@keyframes iconIn {
  from {transform: rotateY(-90deg)}
  to {transform: rotateY(0)}
}
@keyframes iconOut {
  from {transform: rotateY(0)}
  to {transform: rotateY(-90deg)}
}
@keyframes iconFade {
  from {opacity: 0}
  to {opacity: 1}
}
.icon-enter-active {
  animation: iconIn .3s;
}
.icon-leave-active {
  animation: iconOut .3s;
}
.icon-appear-active {
  animation: iconFade .6s;
}
</style>
