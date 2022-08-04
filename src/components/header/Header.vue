<template>
  <header>
    <input
      type="text"
      placeholder="Search..."
      @keyup.enter="$emit('search', $event.target.value)"
    />
  </header>
</template>

<script>
export default {
  emits: ["search"],
};
</script>
