<!------------------------------------------------------------------------------
  - Danbooru Diffusion Prompt Builder
  - Copyright (C) 2022  Jabasukuriputo Wang
  -
  - This program is free software: you can redistribute it and/or modify
  - it under the terms of the GNU Affero General Public License as published by
  - the Free Software Foundation, either version 3 of the License, or
  - (at your option) any later version.
  -
  - This program is distributed in the hope that it will be useful,
  - but WITHOUT ANY WARRANTY; without even the implied warranty of
  - MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
  - GNU Affero General Public License for more details.
  -
  - You should have received a copy of the GNU Affero General Public License
  - along with this program.  If not, see <https://www.gnu.org/licenses/>.
  -
  ----------------------------------------------------------------------------->

<script setup lang="ts">
import { h } from 'vue'
import { isDark } from '../composables/dark'
import { ElSwitch, ElTooltip } from 'element-plus'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import {
    faEye,
    faEyeSlash,
    faLightbulb,
    faShield,
    faTriangleExclamation,
} from '@fortawesome/free-solid-svg-icons'
import {
    faLightbulb as faLightbulbSlash
} from '@fortawesome/free-regular-svg-icons'
import { useSettingsStore } from '../stores/settings'

const settingsStore = useSettingsStore()
const activeIcon = h(FontAwesomeIcon, { icon: faEye })
const inactiveIcon = h(FontAwesomeIcon, { icon: faEyeSlash })

const safeIcon = h(FontAwesomeIcon, { icon: faShield })
const unsafeIcon = h(FontAwesomeIcon, { icon: faTriangleExclamation })

const lightIcon = h(FontAwesomeIcon, { icon: faLightbulb })
const darkIcon = h(FontAwesomeIcon, { icon: faLightbulbSlash })

const ax = h('span', { class: 'switch-text-icon math-style' }, [
    'a',
    h('sup', {}, 'x'),
])
const plus = h('span', { class: 'switch-text-icon' }, ['+'])
</script>

<template>
    <div class="feature-switches">
        <ElTooltip content="暗黑模式" :show-after="750">
            <ElSwitch
                v-model="isDark"
                :active-icon="darkIcon"
                :inactive-icon="lightIcon"
                inline-prompt
                size="large" />
        </ElTooltip>
        <ElTooltip content="显示图片" :show-after="750">
            <ElSwitch
                v-model="settingsStore.showImage"
                :active-icon="activeIcon"
                :inactive-icon="inactiveIcon"
                inline-prompt
                size="large" />
        </ElTooltip>
        <ElTooltip content="步进速率" :show-after="750">
            <ElSwitch
                v-model="settingsStore.useFixedMultiplier"
                :active-icon="plus"
                :inactive-icon="ax"
                inline-prompt
                size="large" />
        </ElTooltip>
        <ElTooltip content="强调类型" :show-after="750">
            <ElSwitch
                v-model="settingsStore.newEmphasis"
                active-text="()"
                inactive-text="{}"
                inline-prompt
                size="large" />
        </ElTooltip>
        <ElTooltip content="分级限制" :show-after="750">
            <ElSwitch
                v-model="settingsStore.showRestricted"
                :active-icon="unsafeIcon"
                :inactive-icon="safeIcon"
                inline-prompt
                class="restricted-switch"
                size="large" />
        </ElTooltip>
    </div>
</template>

<style scoped lang="scss">
.feature-switches {
    display: inline-flex;
    flex-direction: row;
    gap: 1rem;
}
.feature-switches > .restricted-switch {
    --el-switch-on-color: var(--el-color-danger);
    --el-switch-off-color: var(--el-color-success);
}
</style>
