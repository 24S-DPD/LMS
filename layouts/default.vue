<script setup lang="ts">
const route = useRoute()
// const { status } = useAuth()
const isAuthenticated = true // computed(() => status.value === 'authenticated')
const isNavbarCollapsed = ref(false)

const { sidebarOptions, footerOptions } = useSidebarOptions()
const { appName, currentRoute } = useRouteTitle(computed(() => route.path))

useHead({ title: appName })
</script>

<template>
  <div class="flex">
    <n-layout position="absolute" has-sider>
      <n-layout-sider
        v-if="isAuthenticated"
        collapse-mode="width"
        class="flex justify-between py-14"
        :collapsed-width="75"
        :collapsed="isNavbarCollapsed"
        show-trigger="arrow-circle"
        bordered
        @collapse="isNavbarCollapsed = true"
        @expand="isNavbarCollapsed = false"
      >
        <div class="flex flex-col justify-between h-full">
          <div class="shrink-0 ">
            <div class="flex justify-center pb-2">
              <Logo :shrink-logo="isNavbarCollapsed" />
            </div>
            <n-menu
              :options="sidebarOptions"
              :value="currentRoute"
              :collapsed="isNavbarCollapsed"
              :collapsed-width="75"
              :collapsed-icon-size="22"
              :root-indent="20"
              :indent="10"
              accordion
            />
          </div>
          <n-menu
            :options="footerOptions"
            :value="currentRoute"
            :collapsed="isNavbarCollapsed"
            :collapsed-width="70"
            :collapsed-icon-size="22"
            :root-indent="20"
            accordion
            class="shrink-0 mb-4"
          />
        </div>
      </n-layout-sider>
      <n-layout-content>
        <div class="relative min-h-screen grow overflow-auto bg-slate-100 flex items-center justify-center flex-col">
          <slot />
        </div>
      </n-layout-content>
    </n-layout>
  </div>
</template>
