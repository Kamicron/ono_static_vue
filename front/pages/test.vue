<!-- <template>
  <div class="test">
    <h1>News for Team Fortress 2</h1>
    <div v-if="isLoading">Loading...</div>
    <div v-else>
      <ul>
        <li v-for="newsItem in news" :key="newsItem.gid">
          {{ newsItem.title }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';

const news = ref([]);
co
  components: { cards_player },nst isLoading = ref(true);

const getNews = async () => {
  try {
    const response = await axios.get('http://localhost:3001/news');
    news.value = response.data.appnews.newsitems;
  } catch (error) {
    console.error(error);
    news.value = "Erreur lors de la récupération"
  } finally {
    isLoading.value = false;
  }
};

getNews();
</script> -->

<!-- <script setup>
import { ref } from 'vue';
import axios from 'axios';

const playerInfo = ref({});
const steamId = '76561197992709103'; // SteamID du joueur
const url = `http://localhost:3001/api/steam`;

const getPlayerInfo = async () => {
  const response = await axios.get(url, {
    params: {
      steamids: steamId,
    }
  });

  // Utilisation de DOMParser pour convertir la chaîne XML en objet DOM
  const parser = new DOMParser();
  const xmlDoc = parser.parseFromString(response.data, "application/xml");

  // Accéder aux données dans le DOM XML
  const players = xmlDoc.getElementsByTagName("player");
  const player = players[0]; // Ajustez en fonction de vos besoins
  playerInfo.value = {
    steamid: player.getElementsByTagName("steamid")[0].textContent,
    personaname: player.getElementsByTagName("personaname")[0].textContent,
    avatar: player.getElementsByTagName("avatar")[0].textContent,
    profileurl: player.getElementsByTagName("profileurl")[0].textContent,
    // Ajoutez d'autres champs ici
  };

  console.log(playerInfo.value);
}

// Appeler la fonction au démarrage si vous le souhaitez
getPlayerInfo();</script>

<template>
  <div class="test">
    <cardsPlayer :player="playerInfo" />
        <button @click="getPlayerInfo">Click</button>
  </div>
</template>

 -->

 <template>
  <div class="test">
    <h1>Statistiques du joueur pour CS:GO</h1>
    <cards-player v-if="isDataLoaded" :playerData="playerData" :playerStats="transformStats(playerStats.playerstats.stats)"/>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import axios from 'axios';

const steamid = ref('76561197992709103');  // Remplacez par la valeur de votre choix ou liez-la à un élément de votre UI
const playerStats = ref({});
const isDataLoaded = ref(false);

const transformStats = (statsArray) => {
  const obj = {};
  for (let stat of statsArray) {
    obj[stat.name] = stat.value;
  }
  return obj;
};

const getStats = async () => {
  console.log("getStats");
  
  try {
    const response = await axios.get(`http://localhost:3001/api/getStatPlayer?steamid=${steamid.value}`);
    playerStats.value = response.data;
    console.log('playerStats.value',playerStats.value);
    isDataLoaded.value = true;
  } catch (error) {
    console.error("Erreur lors de la récupération des stats du joueur:", error);
  }
};
const playerData = ref({
  pseudo: '',
  playerImage: '',
  profileUrl: ''
});

const getPlayerData = async () => {
  console.log("getPlayerData");

  try {
    console.log("try");
    
    const response = await axios.get(`http://localhost:3001/api/steam?steamids=${steamid.value}`);
    const playerInfo = response.data.response.players[0].player[0];  // Accéder à l'information correcte du joueur
    const pseudo = playerInfo.personaname[0]; // Accéder au premier élément du tableau personaname
    const playerImage = playerInfo.avatarfull[0]; // Accéder au premier élément du tableau avatarfull
    const playerProfileurl = playerInfo.profileurl[0]; // Accéder au premier élément du tableau avatarfull


    playerData.value.pseudo = pseudo;
    playerData.value.playerImage = playerImage;
    playerData.value.profileUrl = playerProfileurl;
    
  } catch (error) {
    console.error("Erreur lors de la récupération des données du joueur:", error);
  }
};

// Appeler la fonction lorsque le composant est monté
onMounted(() => {
  getStats();
  getPlayerData();
});
</script>

<style scoped lang="scss">
.test {
  margin: 300px 50px;
}
</style>