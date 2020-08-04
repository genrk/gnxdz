<template>
  <footer class="footer">
    <div class="content has-text-centered">
      <div class="footpad footer-disclaimer">
        <span class="disclaimer-head">WARNING:</span> &nbsp; Bons estudos.
      </div>
      <div v-if="footerLogo" class="footpad footimage">
        <img width="150" height="75" class="gloryimage" :src="footerLogoLink">
      </div>
      <div class="footpad footicons">
        Github - <a class="icon-tag" href="https://github.com/genrk/gnxdz">akGDz</a> | Support Me!
      </div>
      <div class="footpad footer-copyright">
        Copyright&nbsp;<i class="fas fa-copyright"></i> {{ Date.now() | moment("YYYY") }} | &nbsp;Knowledge must be shared.
      </div>
      <div class="footpad footer-policy">
        Licensed under FrontEnd - <a href="https://github.com/genrk/gnxdz/blob/dark-mode-0-1/LICENSE" target="_blank"> GPL 3.0 </a> | Backend - <a href="https://github.com/genrk/gnxdz/blob/dark-mode-0-1/vuejs/LICENSE" target="_blank">MIT</a>
      </div>
      <div class="footpad footer-code">
        Please Read our <a href="https://github.com/genrk/gnxdz/blob/dark-mode-0-1/CODE_OF_CONDUCT.md" target="_blank">Código de Conduta</a> | <a href="https://raw.githubusercontent.com/genrk/gnxdz/dark-mode-0-1/CONTRIBUTING.md" target="_blank">Termos</a>
      </div>
    </div>
  </footer>
</template>
<script>
export default {
  props: {},
  watch: {},
  data: function () {
    return {
      content: "",
      footerLogo: false,
      footerLogoLink: "",
    };
  },
  components: {},
  methods: {},
  mounted() {
    this.footerLogo = window.themeOptions.footer_logo
    if(this.footerLogo){
      this.footerLogoLink = window.themeOptions.footer_logo_link;
    } else {
      this.footerLogoLink = "";
    }
  },
};
</script>
