<template>
  <div class="range-slider">
    <div class="range-slider__current">{{ value }} %</div>
    <input class="range-slider__input" type="range" :min="min" :max="max" :value="value" :step="step" @input="updateRange">
    <div class="range-slider-buttons" @click="setValue">
      <button class="range-slider__button" data-value="25">25%</button>
      <button class="range-slider__button" data-value="50">50%</button>
      <button class="range-slider__button" data-value="75">75%</button>
      <button class="range-slider__button" data-value="100">100%</button>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'range',
    data () {
      return {
        range: this.value
      }
    },
    props: {
      value: {
        default: 0
      },
      min: {
        type: Number,
        default: 0,
        validator (value) {
          return value >= 0
        }
      },
      max: {
        type: Number,
        default: 100,
        validator (value) {
          return value <= 100
        }
      },
      step: {
        type: Number,
        default: 1
      }
    },
    methods: {
      updateRange (event) {
        this.$emit('input', event.target.value)
      },
      setValue (event) {
        this.range = event.target.dataset.value
      }
    },
    watch: {
      range () {
        this.$emit('input', this.range)
      },
      value () {
        this.range = this.value
      }
    }
  }
</script>

<style>
.range-slider {
  position: relative;
  padding: 15px;
  background-color: #22293c;
  user-select: none;
  font-family: 'Arial', sans-serif;
  color: #fff;
}

.range-slider__input {
  -webkit-appearance: none;
  display: inline-block;
  margin: 0;
  vertical-align: middle;
  width: 100%;
  height: 45px;
  background: none;
  margin: 35px 0;
}

.range-slider__input:focus {
  outline: none;
}

/* Задает стилизацию для элемента прогресса */
.range-slider__input::-webkit-slider-runnable-track {
  height: 100%;
  padding: 0 5px;
  border-radius: 25px;
  background: rgb(68,230,200);
  background: linear-gradient(130deg, rgba(68,230,200,1) 27%, rgba(246,241,64,1) 52%, rgba(255,184,85,1) 70%, rgba(255,104,85,1) 88%);
  cursor: pointer;
  transition: all .2s ease;
}

/* Задаем стилизацию для элемента ползунка */
.range-slider__input::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 35px;
  height: 35px;
  border-radius: 50%;
  background-color: #fff;
  position: relative;
  z-index: 3;
  cursor: pointer;
  transform: translateY(15%);
}

.range-slider__current {
  color: #7e869f;
  font-size: 20px;
  font-weight: 700;
}

.range-slider-buttons {
  text-align: center;
}

.range-slider__button {
  background-color: #55648f;
  border: none;
  outline: none;
  color: #fff;
  font-size: 20px;
  font-weight: 600;
  border-radius: 25px;
  padding: 10px;
  margin-right: 6px;
  cursor: pointer;
  transition: background-color .2s ease-in, box-shadow .2s ease-in;
}

.range-slider__button:focus {
  box-shadow: 0 0 4px 1px #aec3fd;
}

.range-slider__button:hover {
  background-color: #6678aa;
}

.range-slider__button:active {
  background-color: #505e86
}

.range-slider__button:last-child {
  margin-right: 0;
}

@media (min-width: 360px) {
  .range-slider__button {
    margin-right: 15px;
  }
}

@media (min-width: 480px) {
  .range-slider__button {
    padding: 10px 25px;
    margin-right: 25px;
  }
}

@media (min-width: 768px) {
  .range-slider__input {
    margin: 50px 0;
  }

  .range-slider__button {
    font-size: 24px;
  }
}
</style>