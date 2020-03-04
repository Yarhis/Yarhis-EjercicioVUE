<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Login</router-link> ||
      <router-link to="/initstorage">Inicializa Local Storage</router-link>||
    </div>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: rgb(0, 0, 0);
  background-color: rgb(255, 255, 255);
width: 100%;
}

#nav {
  padding: 30px;
  background-color: rgb(236, 161, 62);
   border: solid 0.5em #524e2f;
    border-radius: 6px;
}

#nav a {
  font-weight: bold;
  color: #ebe9cd;
}

#nav a.router-link-exact-active {
  color: #ac1805;
}

label{
  padding: 20px 10px 20px 10px;
    font-weight: bold;
    color: rgb(82, 80, 80);
    font-size: 1.1em;

}
input{
   border-radius: 8px;
   color: rgb(112, 112, 111);
    margin: 5px 5px 5px 5px;
    padding: 10px 10px 10px 10px;

}

button{
    border-radius: 6px;
 background-color: rgb(236, 161, 62);
 color: rgb(255, 255, 255);
    font-weight: bold;
    padding: 5px 5px 5px 5px;

}


</style>
