<template>
  <div class="form-group">
    <label>{{ name }}</label>
    <transition :name="animateIcons">
      <fa-icon v-if="activated" :name="icon" :class="iconClasses"></fa-icon>
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
    },
    animateIcons () {
      return this.valid ? 'rotate' : 'fade';
    }
  },
  methods: {
    onInput (e) {
      this.activated = true;
      this.$emit('updated', e.target.value);
      console.log(this.valid);
    }
  }
}
</script>
<style>
@keyframes fade {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
@keyframes rotate {
  0% {
    transform: rotateY(0);
  }
  100% {
    transform: rotateY(720deg);
  }
}
.fade-enter-active {
  animation: fade .3s ease-in;
}
.fade-leave-active {
  animation: fade .3s ease-in reverse;
}
.rotate-enter-active {
  animation: rotate 1s ease-in;
}
.rotate-leave-active {
  animation: rotate 1s ease-in reverse;
}
</style>
