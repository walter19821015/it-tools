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
import CollapsibleToolMenu from '@/components/CollapsibleToolMenu.vue';

const themeVars = useThemeVars();
const styleStore = useStyleStore();
const version = config.app.version;
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
          v{{ version }}
        </div>
      </div>
    </template>

    <template #content>
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
        </div>

        <div class="right">
          <NavbarButtons />
        </div>
      </div>

      <slot />
    </template>
  </MenuLayout>
</template>

<style lang="less" scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
  border-bottom: 1px solid v-bind('themeVars.borderColor');

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
    padding: 20px;
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
      font-weight: bold;
      color: #fff;
      z-index: 1;
    }

    .subtitle {
      position: relative;
      font-size: 12px;
      color: rgba(255, 255, 255, 0.8);
      z-index: 1;
    }
  }

  .footer {
    padding: 15px;
    font-size: 11px;
    opacity: 0.6;
    margin-top: auto;
    text-align: center;
  }
}
</style>
