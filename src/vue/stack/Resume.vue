<template>
    <div v-if="didLoadAllJsonFiles" id="resume">
        <NavigationWrapper>
            <Section v-for="(section, index) in sections" :key="index"
                     :presentation-mode="String(presentationMode)"
                     :model="section"
                     :active="_isSectionActive(section)"/>
        </NavigationWrapper>
    </div>
</template>

<script setup>
import {inject, onMounted} from "vue"
import Section from "/src/vue/components/sections/Section.vue"
import NavigationWrapper from "/src/vue/components/navigation/NavigationWrapper.vue"
import {useUtils} from "/src/composables/utils.js"

const utils = useUtils()

/** @type {{value: Boolean}} */
const didLoadAllJsonFiles = inject("didLoadAllJsonFiles")

/** @type {{value: String}} */
const presentationMode = inject("presentationMode")

/** @type {{value: Section[]}} */
const sections = inject("sections")

/** @type {{value: Section}} */
const currentSection = inject("currentSection")

/**
 * @description This hook can be used to report a visit to an external analytics service.
 * Here, you can integrate Google Analytics, Mixpanel, or your own custom analytics implementation.
 */
const _isSectionActive = (section) => {
    if(!currentSection.value)
        return false
    return currentSection.value.id === section.id
}
</script>

<style lang="scss" scoped>
@import "/src/scss/_theming.scss";

#resume {
    display: flex;
    min-height: 100vh;
    background-color: $nav-background;
    @include media-breakpoint-down($navigation-sidebar-breakpoint) {
        background-color: $default-section-background;
    }
}
</style>