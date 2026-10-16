<script lang="ts" setup>
import { NIcon, useThemeVars } from 'naive-ui';
import { RouterLink } from 'vue-router';
import { Home2, Menu2 } from '@vicons/tabler';

import { storeToRefs } from 'pinia';
import HeroGradient from '../assets/hero-gradient.svg?component';
import MenuLayout from '../components/MenuLayout.vue';
import NavbarButtons from '../components/NavbarButtons.vue';
import { useStyleStore } from '@/stores/style.store';
import { config } from '@/config';
import type { ToolCategory } from '@/tools/tools.types';
import { useToolStore } from '@/tools/tools.store';
import { useTracker } from '@/modules/tracker/tracker.services';
import CollapsibleToolMenu from '@/components/CollapsibleToolMenu.vue';

const themeVars = useThemeVars();
const styleStore = useStyleStore();
const version = config.app.version;
const commitSha = config.app.lastCommitSha.slice(0, 7);

const tracker = useTracker();
const toolStore = useToolStore();
const { isSmallScreen } = storeToRefs(styleStore);
</script>

<template>
  <MenuLayout>
    <template #sider>
      <div class="sider-content">
        <RouterLink to="/" class="logo">
          <HeroGradient class="hero-gradient" />
          <div class="title">
            IT - TOOLS
          </div>
          <div class="subtitle">
            {{ $t('home.subtitle') }}
          </div>
        </RouterLink>

        <CollapsibleToolMenu />

        <div class="footer">
          <a
            :href="`https://github.com/CorentinTh/it-tools/releases/tag/v${version}`"
            target="_blank"
            rel="noopener noreferrer"
          >
            v{{ version }}
          </a>
          <span v-if="commitSha">
            -
            <a
              :href="`
