<template>
  <footer class="site-footer" role="contentinfo">
    <div class="container">
      <div class="footer-bottom">
        <div class="footer-copy">© Savreh 2025</div>
      </div>
    </div>
  </footer>
</template>

<script setup>
</script>

<style scoped>
.site-footer {
  position: relative;
  background: linear-gradient(180deg,#061a48 0%, #0a213f 100%);
  color:#fff;
  padding: 1.25rem 0 1.25rem 0; 
  box-sizing: border-box;
  width: 100%;
  padding-left: 0;
}
.container { max-width:1100px; margin:0 auto; width:100%; padding-left: 0; }

.footer-bottom {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  width: 100%;
}
.footer-copy {
  color: rgba(255,255,255,0.85);
  font-weight: 500;
  margin-left: 0;
  padding-left: 0;
  margin-left: -202px;
}

@media (max-width:900px) {
  .site-footer { padding: 0.75rem 0; }
  .footer-copy { font-size: 0.95rem; margin-left: 0; }
}
</style>
