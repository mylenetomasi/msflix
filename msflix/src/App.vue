<template>
  <header>
    <router-link to="/">
      <h1><span>MS </span>FLIX</h1>
    </router-link>
  </header>
  <main>
    <router-view />
  </main>
  <footer>
    <div class="footer">
      <h1>Mylene e Sarah</h1> <br>
      <h2>2 Info 2</h2>
    </div>
  </footer>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Fira Sans", sans-serif;
}
body {
  background-color: rgb(255, 255, 255);
}
a {
  text-decoration: none;
}
header {
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: white;
  box-shadow: 0px, 0px, 6px rgba(0, 0, 0, 0.1);
}
h1 {
  color: black;
  font-size: 36px;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  font-weight: bold;
  span {
    color: rgb(163, 1, 152);
  }
}
footer {
  display: flex;
  flex-direction: row;
  background-color: rgb(163, 1, 152);
  height: 290px;
  justify-content: center;
  color: white;
}
footer .footer h1 {
  color: white;
  font-weight: bold;
  margin-top: 100px;
}
footer .footer h2 {
  color: white;
  font-weight: bold;
  margin-left: 100px;
}
</style>
