<script setup lang="ts">
const props = defineProps<{
  content: string;
  href: string;
  svg?: string;
}>();

function redirect(uri: string) {
  window.location.href = uri;
}
</script>

<template>
  <li class="suggestion" :class="{ intelligence: !!props.svg }">
    <a :href="props.href" @click="redirect(props.href)">
      <p v-if="props.svg" v-html="props.svg" />
      <span>{{ props.content }}</span>
      <slot />
    </a>
  </li>
</template>

<style>
.suggestion {
  padding: 2px 10px;
  transition: 0.3s;
  cursor: pointer;
  border-radius: 6px;
}

.suggestion:hover {
  background: rgba(255, 255, 255, 0.1);
}

.suggestion a {
  display: flex;
  flex-direction: row;
  color: #fff;
  text-decoration: none;
  transition: 0.25s;
  will-change: transform;
}

.suggestion:hover a {
  transform: translateX(12px);
}
.suggestion p svg {
  width: 16px;
  height: 16px;
  fill: rgba(255, 255, 255, 0.8);
  transform: translateY(2px);
}

.intelligence span {
  color: rgba(255, 255, 255, 0.95);
  margin-left: 6px;
  display: inline-block;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>
