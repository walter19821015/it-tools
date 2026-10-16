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
        </div>
      </div>
    </template>

    <template #content>
      <slot name="content-header">
        <div class="header">
          <div class="left">
            <c-button
              v-if="isSmallScreen"
              circle
              variant="text"
              aria-label="Toggle menu"
              @click="styleStore.toggleMenu"
            >
              <NIcon size="25" :component="Menu2" />
            </c-button>
            <RouterLink to="/">
              <c-button circle variant="text" aria-label="Home">
                <NIcon size="25" :component="Home2" />
              </c-button>
            </RouterLink>
            <slot name="header-left" />
          </div>

          <div class="right">
            <slot name="header-right" />
            <NavbarButtons />
          </div>
        </div>
      </slot>

      <slot />
    </template>
  </MenuLayout>
</template>

<style lang="less" scoped>
.header {
  border-bottom: 1px solid v-bind('themeVars.borderColor');
  padding: 10px 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;

  .left,
  .right {
    display: flex;
    align-items: center;
    gap: 10px;
  }
}

.sider-content {
  display: flex;
  flex-direction: column;
  height: 100%;

  .logo {
    display: block;
    position: relative;
    padding: 24px 20px;
    text-decoration: none;
    overflow: hidden;

    .hero-gradient {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 0;
    }

    .title {
      position: relative;
      font-size: 24px;
      font-weight: 900;
      color: #fff;
      z-index: 1;
      line-height: 1.2;
    }

    .subtitle {
      position: relative;
      font-size: 13px;
      color: rgba(255, 255, 255, 0.85);
      z-index: 1;
      margin-top: 4px;
    }
  }

  .footer {
    padding: 16px;
    font-size: 12px;
    opacity: 0.6;
    margin-top: auto;
    text-align: center;

    a {
      color: inherit;
      text-decoration: none;
      &:hover {
        text-decoration: underline;
      }
    }
  }
}
</style>
