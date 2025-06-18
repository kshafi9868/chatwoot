<script>
export default {
  props: {
    disableBranding: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {
      globalConfig: {
        brandName: 'AVR Expos',
        //logoThumbnail: 'https://avrexpos.com/logo-icon.png', // replace with your actual logo URL
        widgetBrandURL: 'https://avrexpos.com',
      },
    };
  },
  computed: {
    brandRedirectURL() {
      try {
        const referrerHost = this.$store?.getters['appConfig/getReferrerHost'];
        const baseURL = `https://avrexpos.com`;
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
      
      <span>
        {{ globalConfig.brandName }}
      </span>
    </a>
  </div>
  <div v-else class="p-3" />
</template>
