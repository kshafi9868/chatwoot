<script>
export default {
  props: {
    disableBranding: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      globalConfig: {
        brandName: 'AVR Expos',
        logoThumbnail: 'https://avrexpos.com/logo-icon.png', // replace with your actual logo URL
        widgetBrandURL: 'https://avrexpos.com',
      },
    };
  },
  computed: {
    brandRedirectURL() {
      try {
        const referrerHost = this.$store?.getters['appConfig/getReferrerHost'];
        const baseURL = `https://webmaster.solutions?utm_source=${
          referrerHost ? 'widget_branding' : 'survey_branding'
        }`;
        return baseURL;
      } catch (e) {
        return 'https://avrexpos.com';
      }
    },
  },
};
</script>

<template>
  <div
    v-if="globalConfig.brandName && !disableBranding"
    class="px-0 py-3 flex justify-center"
  >
    <a
      :href="brandRedirectURL"
      rel="noreferrer noopener nofollow"
      target="_blank"
      class="branding--link text-n-slate-11 hover:text-n-slate-12 cursor-pointer text-xs inline-flex grayscale-[1] hover:grayscale-0 hover:opacity-100 opacity-90 no-underline justify-center items-center leading-3"
    >
      <img
        class="ltr:mr-1 rtl:ml-1 max-w-3 max-h-3"
        :alt="globalConfig.brandName"
        :src="globalConfig.logoThumbnail"
      />
      <span>
        {{ globalConfig.brandName }}
      </span>
    </a>
  </div>
  <div v-else class="p-3" />
</template>
