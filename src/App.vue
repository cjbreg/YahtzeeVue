<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: left;
  color: #8a7432;
  padding: 24px;
}
body {
  min-height: 100vh;
  background: #055037 !important;
  box-shadow: inset 0px 0px 50px #023424;
  background-attachment: fixed;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

@font-face {
  font-family: "Rubik One";
  src: local("Rubik One"),
    url(./fonts/Rubik_Mono_One/RubikMonoOne-Regular.ttf) format("truetype");
}

@font-face {
  font-family: "Montserrat Alternates";
  src: local("Montserrat Alternates"),
    url(./fonts/Montserrat_Alternates/MontserratAlternates-Regular.ttf)
      format("truetype");
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
