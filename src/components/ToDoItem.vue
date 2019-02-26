<template>
  <div>
    {{todo.title}}
    <span :id="todo.id" @click="removeItem">x</span>
  </div>
</template>
<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
  methods: {
    removeItem(event) {
      this.$emit('remove', event.target.id);
    },
  },
};
</script>
