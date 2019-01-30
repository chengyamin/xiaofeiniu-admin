<template>
  <div id="app">
      <h3>{{1000 | date}}</h3>
      <h3>{{1000 | datetime}}</h3>
      <h3>{{1000 | currency}}</h3>
    <router-view/>
  </div>
</template>

<style lang="">

</style>
