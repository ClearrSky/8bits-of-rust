<!-- 创作页面 -->
<template>
  <div>
    <div class="container">
      <my-button
        text="插件"
        :active="isComposePage('plugin')"
        @click="changeComposePage('plugin')"
      />
      <my-button
        text="混音台"
        :active="isComposePage('mixer')"
        @click="changeComposePage('mixer')"
      />
      <my-button
        text="编曲"
        :active="isComposePage('arrangement')"
        @click="changeComposePage('arrangement')"
      />
      <my-button
        text="导出歌曲"
        :active="isComposePage('export')"
        @click="changeComposePage('export')"
      />
      <play-unit class="play-unit" />
    </div>

    <div class="placeholder-block"></div>
    <div class="main-container">
      <plugin v-if="isComposePage('plugin')"></plugin>
      <mixer v-if="isComposePage('mixer')"></mixer>
      <arrangement v-if="isComposePage('arrangement')"></arrangement>
      <export-song v-if="isComposePage('export')"></export-song>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import { useStore } from "vuex";

import Plugin from "@/components/compose/Plugin.vue";
import Mixer from "@/components/compose/Mixer.vue";
import Arrangement from "@/components/compose/Arrangement.vue";
import ExportSong from "@/components/compose/ExportSong.vue";
import PlayUnit from "@/components/playUnit/PlayUnit.vue";

// 通过store.state.activeComposePage选择显示的子页面
const store = useStore();

const isComposePage = computed(
  () => (page) => store.state.route.activeComposePage === page,
);

const changeComposePage = (page) => {
  store.commit("route/setActiveComposePage", page);
};
</script>

<style>
.container {
  display: flex;
  flex-direction: row;
  align-items: center;
  width: 100%;
  gap: 6px;
}

.placeholder-block {
  height: 50px;
}
</style>
