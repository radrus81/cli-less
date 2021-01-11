<template>
  <div class="card">
    <h3>{{ title }} | {{ titleAll }}</h3>

    <app-button color="primary" @action="open">{{
      isNewsOpen ? 'Close' : 'Open'
    }}</app-button>
    <div v-if="isNewsOpen">
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Doloribus
        numquam nisi tempore, quos a fugit inventore fugiat praesentium ducimus
        aliquam illo ad, consectetur corporis et quia hic, ex incidunt error.
      </p>
      <hr />

      <app-button
        v-if="!wasRead"
        color="primary"
        @action="$emit('readed-news', this.id)"
        >Прочитал</app-button
      >
    </div>
  </div>
</template>

<script>
import AppButton from './AppBtn'
export default {
  // props: ['title'],
  props: {
    id: Number,
    title: { type: String, required: true },
    isOpen: {
      type: Boolean,
      required: false,
      default: false,
      // validator(value) {
      //   return false //если false то валидация не прошла
      // },
    },
    wasRead: Boolean,
  },
  inject: ['titleAll', 'newsAll'],
  //emits: ['open-news'],
  emits: {
    //'open-news':null если не нужно валидировать, то null
    'open-news': null,
    'readed-news'(id) {
      if (id) {
        return true
      }
      console.log('Нет параметра id')
    },
  },
  data() {
    return {
      isNewsOpen: this.isOpen,
    }
  },
  methods: {
    open() {
      this.isNewsOpen = !this.isNewsOpen
      if (this.isNewsOpen) {
        this.$emit('open-news')
      }
    },
    readed() {
      this.isNewsOpen = false
      this.$emit('readed-news', this.id)
    },
  },
  components: {
    AppButton,
  },
}
</script>
