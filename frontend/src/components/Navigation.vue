<template>
  <b-menu-list>
    <b-menu-item :to="{ name: 'dashboard' }" tag="router-link" :active="activeItem.dashboard"
      icon="view-dashboard-variant-outline" :label="$t('menu.dashboard')" /><!-- dashboard -->


    <b-menu-item :to="{ name: 'lists' }" tag="router-link" :active="activeItem.lists"
  data-cy="lists" icon="format-list-bulleted-square" :label="$t('User Category')" />
  <!-- User Category -->


    <b-menu-item :to="{ name: 'subscribers' }" tag="router-link" :active="activeItem.subscribers"
  data-cy="subscribers" icon="account-multiple" :label="$t('Users')" />
    <!-- Users -->


    <b-menu-item :expanded="activeGroup.campaigns" :active="activeGroup.campaigns" data-cy="campaigns"
      @update:active="(state) => toggleGroup('campaigns', state)" icon="rocket-launch-outline"
      :label="$t('Newsletter')">
      <b-menu-item :to="{ name: 'campaigns' }" tag="router-link" :active="activeItem.campaigns" data-cy="all-campaigns"
        icon="rocket-launch-outline" :label="$t('All Newsletters')" />
      <b-menu-item :to="{ name: 'campaign', params: { id: 'new' } }" tag="router-link" :active="activeItem.campaign"
        data-cy="new-campaign" icon="plus" :label="$t('New Newsletter')" />
      <b-menu-item :to="{ name: 'media' }" tag="router-link" :active="activeItem.media" data-cy="media"
        icon="image-outline" :label="$t('menu.media')" />
      <b-menu-item :to="{ name: 'templates' }" tag="router-link" :active="activeItem.templates" data-cy="templates"
        icon="file-image-outline" :label="$t('globals.terms.templates')" />
      <b-menu-item :to="{ name: 'campaignAnalytics' }" tag="router-link" :active="activeItem.campaignAnalytics"
        data-cy="analytics" icon="chart-bar" :label="$t('globals.terms.analytics')" />
    </b-menu-item><!-- campaigns -->

    <b-menu-item :expanded="activeGroup.settings" :active="activeGroup.settings" data-cy="settings"
      @update:active="(state) => toggleGroup('settings', state)" icon="cog-outline" :label="$t('menu.settings')">
      <b-menu-item :to="{ name: 'settings' }" tag="router-link" :active="activeItem.settings" data-cy="all-settings"
        icon="cog-outline" :label="$t('menu.settings')" />
      <b-menu-item :to="{ name: 'maintenance' }" tag="router-link" :active="activeItem.maintenance" data-cy="maintenance"
        icon="wrench-outline" :label="$t('menu.maintenance')" />
      <b-menu-item :to="{ name: 'logs' }" tag="router-link" :active="activeItem.logs" data-cy="logs"
        icon="newspaper-variant-outline" :label="$t('menu.logs')" />
    </b-menu-item><!-- settings -->

    <b-menu-item v-if="isMobile" icon="logout-variant" :label="$t('users.logout')" @click.prevent="doLogout" />
  </b-menu-list>
</template>

<script>
export default {
  name: 'Navigation',

  props: {
    activeItem: { type: Object, default: () => { } },
    activeGroup: { type: Object, default: () => { } },
    isMobile: Boolean,
  },

  methods: {
    toggleGroup(group, state) {
      this.$emit('toggleGroup', group, state);
    },

    doLogout() {
      this.$emit('doLogout');
    },
  },

  mounted() {
    // A hack to close the open accordion burger menu items on click.
    // Buefy does not have a way to do this.
    if (this.isMobile) {
      document.querySelectorAll('.navbar li a[href]').forEach((e) => {
        e.onclick = () => {
          document.querySelector('.navbar-burger').click();
        };
      });
    }
  },
};

</script>
