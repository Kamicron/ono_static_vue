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

<style scoped lang="scss">
.test {
  margin: 300px 50px;
}
</style> -->

<script setup>
import { ref } from 'vue';
import axios from 'axios';

const steamApiKey = 'YOUR_STEAM_API_KEY'; // Remplacez par votre clé API
const steamId = '76561198207453521'; // SteamID du joueur
const gameId = 730; // ID de CS:GO
const playerStats = ref({});

const url = `http://api.steampowered.com/ISteamUserStats/GetUserStatsForGame/v0002/?appid=${gameId}&key=${steamApiKey}&steamid=${steamId}`;

const getPlayerStats = async () => {
  try {
    const response = await axios.get(url);
    playerStats.value = response.data.playerstats;
  } catch (error) {
    console.error('Erreur lors de la récupération des statistiques du joueur:', error);
  }
};

getPlayerStats();
</script>

<template>
  <div>
    <h1>Statistiques du joueur pour CS:GO</h1>
    <!-- Vous pouvez maintenant utiliser playerStats dans votre template pour afficher les données -->
  </div>
</template>
