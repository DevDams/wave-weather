<template>
  <div class="about">
    <div class="container">
      <h1>A porpos de Wave Weather 🌧</h1>
      <p>
        Wave Weather est un outil permettant de connaitre la météo dans une ville. <br>
        Par défaut, si vous n'avez effectué aucune recherche, la météo affichée est celle de votre position actuelle. <br>
        De ce fait, l'autorisation de la location sur votre appareil est nécessaire pour une expérience optimale. <br><br>
        L'utilisation de wave weather est simple, tout ce que vous avez à faire c'est rechercher le nom de la ville dont vous aimeriez savoir la météo
        et attendre que les resultats de votre recherche s'affiche. <br> Et voilà !!! 👌
      </p>
    </div>
  </div>
</template>

<style scoped>
body {
  text-align: center;
}

.about {
  text-align: center !important;
  margin-bottom: 100px;
}

h1 {
  font-size: 60px;
  font-family: 'Bebas Neue', cursive;
  text-transform: uppercase;
  margin-top: 80px;
  color: #4B856C;
}

p {
  width: 80%;
  margin: auto;
  margin-top: 50px;
  font-size: 24px;
  line-height: 35px;
  color: black;
}

@media (max-width: 621px) {
  h1 {
    font-size: 55px;
  }

  p {
    font-size: 21px;
  }
}

@media (max-width: 465px) {
  h1 {
    font-size: 45px;
  }
  
  p {
    font-size: 18px;
    line-height: 28px;
  }
}
</style>
