<template>
  <section style="width: 100%">
    <full-page>
      <section class="section" style="background: #f59e0b">
        <div>Page one</div>
      </section>
      <section class="section" style="background: #ef4444">
        <div>Page Two</div>
      </section>
      <section class="section" style="background: #001122">
        <div>Page Three</div>
      </section>
    </full-page>
  </section>
</template>

<script>
export default {};
</script>

<style scoped>
.section {
  height: 100vh;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 25px;
}
</style>