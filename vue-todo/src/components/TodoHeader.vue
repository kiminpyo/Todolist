<template>
  <div>
    <header>
      <h1>TODO it!</h1>
    </header>
  </div>
</template>

<script>
export default {

}
</script>
<!--scoped ===> 싱글컴포넌트 안에서만 유효한 속성 (부모 영향x)-->
<style scoped>
h1{
  color: #2F3B52;
  font-weight: 900;
  margin: 2.5rem 0 1.5rem;
}
</style>