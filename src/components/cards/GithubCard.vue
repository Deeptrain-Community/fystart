<script setup lang="ts">
import { data, update, loading } from "@/assets/script/card/github";
import Star from "@/components/icons/star.vue";
import { ref } from "vue";
import Loader from "@/components/icons/loader.vue";

const element = ref<HTMLElement | null>(null);
update();
</script>

<template>
  <div class="card">
    <div class="github-top">
      <span class="github-name">GitHub</span>
      <span style="flex-grow: 1" />
      <span class="github-explore" @click="update">
        <loader v-if="loading" />
        <template v-else>Explore</template>
      </span>
    </div>
    <div class="github-content" ref="element">
      <template v-for="(repo, idx) in data" :key="idx">
        <div class="github-repo">
          <a class="github-header" :href="repo.url" target="_blank">
            <img class="github-avatar" :src="repo.avatar" alt="" />
            <span class="github-user">{{ repo.user }}</span>
            <span class="github-split">/</span>
            <span class="github-repo-name">{{ repo.repo }}</span>
          </a>
          <div class="github-desc">{{ repo.description }}</div>
          <div class="github-footer">
            <star /> <span class="star">{{ repo.stars }}</span>
            <div class="color" :style="{ background: repo.color }" />
            <div class="language">{{ repo.language }}</div>
          </div>
        </div>
      </template>
    </div>
    <div class="github-bottom">
      <span class="github-line"></span>
    </div>
  </div>
</template>

<style scoped>
.card {
  color: #fff;
  position: relative;
  display: flex;
  padding: 4px;
  flex-direction: column;
  background: rgba(13, 17, 23, 0.98);
  backdrop-filter: blur(2px);
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  width: 220px;
  height: 180px;
  margin: 15px 15px 30px 15px;
  transition: 0.3s;
  border-radius: 12px;
  overflow: hidden;
  font-family: var(--fonts);
  user-select: none;
}

.github-name {
  font-family: var(--fonts-en);
}

.github-top {
  display: flex;
  flex-direction: row;
  padding: 0.5em 0.7em 0.3em;
  height: max-content;
  width: 100%;
}

.github-repo {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: max-content;
  padding: 6px 4px;
  animation: FadeInAnimation 0.25s ease-in-out;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.github-repo:last-child {
  border-bottom: none;
}

.github-header {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  height: max-content;
  width: 100%;
  text-decoration: none;
}

.github-avatar {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  margin-right: 5px;
}

.github-user {
  font-size: 14px;
  vertical-align: center;
  text-align: left;
  color: #fff;
  text-decoration: none;
}

.github-header:hover .github-user {
  text-decoration: underline;
}

.github-split {
  font-size: 12px;
  display: inline-block;
  vertical-align: center;
  color: #ccc;
  padding: 2px 4px;
  border-radius: 4px;
  text-decoration: none;
}

.github-repo-name {
  font-size: 14px;
  vertical-align: center;
  color: #fff;
  text-decoration: none;
}

.github-header:hover .github-repo-name {
  text-decoration: underline;
}

.github-desc {
  font-size: 12px;
  text-align: left;
  padding: 4px 0;
}

.github-explore {
  font-size: 12px;
  display: inline-block;
  vertical-align: center;
  background: rgba(56, 140, 255, 0.8);
  padding: 2px 6px;
  border-radius: 4px;
  cursor: pointer;
  user-select: none;
  transition: 0.3s;
}

@keyframes ScrollAnimation {
  from {
    rotate: 0deg;
  }
  to {
    rotate: 360deg;
  }
}

.github-explore svg {
  width: 18px;
  height: 18px;
  margin: 1px 4px -5px;
  fill: #fff;
  animation: ScrollAnimation 1s linear infinite;
}

.github-explore:hover {
  background: rgba(56, 140, 255, 1);
}

.github-content {
  display: flex;
  flex-direction: column;
  padding: 0 0.7em;
  flex-grow: 1;
  width: 100%;
  overflow-x: hidden;
  overflow-y: auto;
}

.github-footer {
  display: flex;
  flex-direction: row;
  padding: 4px 0;
  height: max-content;
  width: 100%;
  align-items: center;
}

.github-footer svg {
  width: 12px;
  height: 12px;
  margin-right: 4px;
  fill: #bbb;
}

.github-footer .star {
  font-size: 12px;
  white-space: nowrap;
  color: #bbb;
  user-select: none;
  margin-right: 12px;
}

.github-footer .color {
  width: 12px;
  height: 12px;
  margin-right: 4px;
  border-radius: 50%;
}

.github-footer .language {
  font-size: 12px;
  white-space: nowrap;
  color: #bbb;
  user-select: none;
}

.github-bottom {
  display: flex;
  flex-direction: row;
  padding: 0.3em 0.7em 0.5em;
  height: max-content;
  width: 100%;
}

.github-line {
  font-size: 12px;
  margin-left: auto;
  display: inline-block;
  vertical-align: center;
  background: #ccc;
  padding: 2px 6px;
  border-radius: 4px;
}
</style>
