<script setup lang="ts">
const { command } = defineProps<{
  command?: boolean
}>()
const { notifications } = useNotifications()
</script>

<template>
  <nav sm:px3 flex="~ col gap2" shrink text-size-base leading-normal md:text-lg>
    <div shrink hidden sm:block mt-4 />
    <SearchWidget lg:ms-1 lg:me-5 hidden xl:block />
    <NavSideItem :text="$t('nav.search')" to="/search" icon="i-ri:search-line" xl:hidden :command="command" />

    <div shrink hidden sm:block mt-4 />
    <NavSideItem :text="$t('nav.home')" to="/home" icon="i-ri:home-5-line" user-only :command="command" />
    <NavSideItem :text="$t('nav.notifications')" to="/notifications" icon="i-ri:notification-4-line" user-only :command="command">
      <template #icon>
        <div flex relative>
          <div class="i-ri:notification-4-line" text-xl />
          <div v-if="notifications" class="top-[-0.3rem] right-[-0.3rem]" absolute font-bold rounded-full h-4 w-4 text-xs bg-primary text-inverted flex items-center justify-center>
            {{ notifications < 10 ? notifications : '•' }}
          </div>
        </div>
      </template>
    </NavSideItem>
    <NavSideItem :text="$t('nav.conversations')" to="/conversations" icon="i-ri:at-line" user-only :command="command" />
    <NavSideItem :text="$t('nav.favourites')" to="/favourites" icon="i-ri:heart-3-line" user-only :command="command" />
    <NavSideItem :text="$t('nav.bookmarks')" to="/bookmarks" icon="i-ri:bookmark-line" user-only :command="command" />
    <NavSideItem :text="$t('action.compose')" to="/compose" icon="i-ri:quill-pen-line" user-only :command="command" />

    <div shrink hidden sm:block mt-4 />
    <NavSideItem :text="$t('nav.explore')" :to="isHydrated ? `/${currentServer}/explore` : '/explore'" icon="i-ri:hashtag" :command="command" />
    <NavSideItem :text="$t('nav.local')" :to="isHydrated ? `/${currentServer}/public/local` : '/public/local'" icon="i-ri:group-2-line " :command="command" />
    <NavSideItem :text="$t('nav.federated')" :to="isHydrated ? `/${currentServer}/public` : '/public'" icon="i-ri:earth-line" :command="command" />
    <NavSideItem :text="$t('nav.lists')" :to="`/${currentServer}/lists`" icon="i-ri:list-check" :command="command" />

    <div shrink hidden sm:block mt-4 />
    <NavSideItem :text="$t('nav.settings')" to="/settings" icon="i-ri:settings-3-line" :command="command" />
  </nav>
</template>
