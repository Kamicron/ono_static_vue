<template>
  <div v-if="playerStats">
    <div class="player">
      <div class="player__inner">
        <div class="player__information">
          <div class="player__information-name">
            <h2 class="player__information-name--role">Team Elite</h2>
            <h3 class="player__information-name--pseudo">{{ playerData.pseudo }}</h3>
          </div>
          <img :src="playerData.playerImage" alt="Joueur" class="player__information-image"
            v-if="playerData.playerImage" />
        </div>
        <div class="player-stats">
          <div class="player-stats_alltime">

          </div>
          <div class="player-stats__winrate">
            <WidgetsGraphCirc display="% de victoire" :value="props.playerStats.lifetime['Win Rate %']" />
            <WidgetsGraphCirc display="% de headshot" :value="props.playerStats.lifetime['Average Headshots %']" />
          </div>
          <div class="player-stats__kd">
            <p>Ratio K/D: </p>
            <p><strong>{{ playerStats.lifetime["Average K/D Ratio"] }}</strong></p>
          </div>
          <div class="player-stats__recent-results">
            <div class="title">Résultats récents: </div>
            <div class="results__forme">
              <div v-for="(result, index) in props.playerStats.lifetime['Recent Results']"
                :key="index">
                <span v-if="result === '1'">✅</span>
                <span v-else-if="result === '0'">❌</span>
              </div>
            </div>
          </div>
          <div class="player-stats__matches">
            Matches joués: {{ playerStats.lifetime.Matches }} | Matches gagnés: {{ playerStats.lifetime.Wins }}
          </div>
          <div class="player-stats__headshots">
            % de HS: {{ playerStats.lifetime["Total Headshots %"] }}
          </div>

          <div class="player-stats__best-maps">
            <div v-for="segment in bestMaps" :key="segment.label" class="player-stats__map">
              <img :src="segment.img_regular" alt="Image de la carte">
              <div>K/D Ratio: {{ segment.stats["K/D Ratio"] }}</div>
              <div>% HS: {{ segment.stats["Total Headshots %"] }}</div>
              <div>Matches joués: {{ segment.stats.Matches }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div v-else>
    Chargement...
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

// Définir les props
const props = defineProps({
  playerStats: {
    type: Object,
    required: true
  },
  playerData: {  // Ajoutez cette partie
    type: Object,
    required: true
  }
});


if (props.playerStats && props.playerStats.lifetime) {
  console.log('props.playerData', props.playerData);
}

// Vous n'avez plus besoin d'utiliser `.value` avec `playerStats` car il n'est pas un `ref`.
const bestMaps = computed(() => {
  if (props.playerStats && props.playerStats.segments) {
    return props.playerStats.segments.sort((a, b) => parseFloat(b.stats["Win Rate %"]) - parseFloat(a.stats["Win Rate %"])).slice(0, 3);
  }
  return [];
});

</script>

<style lang="scss" scoped>
.player {
  width: 550px;
  background-color: $background-color;
  padding: $spacing-m;
  box-shadow: 0 $spacing-s $spacing-m rgba($black, 0.1);
  text-align: center;
  font-family: $font-main;
  position: relative;

  // Bordure en haut
  &::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0; // Pour commencer du coin gauche
    right: 0;
    height: 5px;
    background: linear-gradient(135deg, transparent calc(15% - 5px), white calc(15% - 5px), white 100%);
  }

  // Bordure à gauche
  &::after {
    content: "";
    position: absolute;
    top: 1%;
    left: 0;
    bottom: 0;
    width: 5px;
    background: linear-gradient(135deg, transparent calc(15% - 2.5px), white calc(15% - 2.5px), white 100%);
  }

  &__inner {

    // Bordure à droite
    &::before {
      content: "";
      position: absolute;
      top: 0;
      right: 0;
      bottom: 10%;
      width: 5px;
      background: linear-gradient(135deg, white 0%, white calc(94% - 5px), transparent calc(94% - 5px));
    }

    // Bordure en bas
    &::after {
      content: "";
      position: absolute;
      bottom: 0;
      left: 0;
      right: 10%;
      height: 5px;
      background: linear-gradient(135deg, white 0%, white calc(94% - 5px), transparent calc(94% - 5px));
    }
  }

  &__information {
    display: flex;
    justify-content: space-around;
    align-items: center;

    &-name {
      &--role {
        margin: 0;
        font-size: $font-size-xl;
        font-family: $font-button;
        text-transform: uppercase;
        font-weight: $font-weight-medium;
        color: $main-color;
      }

      &--pseudo {
        margin: 0;
        font-size: $font-size-xxl;
        font-family: $font-button;
        text-transform: uppercase;
        font-weight: $font-weight-medium;
        color: $secondary-color;
      }

    }

    &-image {
      width: 30%;
      height: auto;
      border-radius: 50%;
      margin-top: $spacing-m;
      border: 2px solid $background-color;
    }
  }
}

.player-stats {
  &__winrate {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  &__kd {
    
    color: $white;
    display: flex;
    justify-content: space-between;
    margin: 0 20%;

    strong {
      color: $secondary-color;
    }
  }

  &__recent-results {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 0 20%;
    
    .title {
    color: $white;
  }
    .results__forme {
      display: flex;

    }
    h3 {
      color: $white;
    }

    /* Styles pour résultats récents */
  }

  &__matches {
    /* Styles pour matches */
  }

  &__headshots {
    /* Styles pour HS % */
  }

  &__best-maps {
    /* Styles pour les meilleures cartes */
  }

  &__map {
    /* Styles pour une seule carte */
  }
}

.donut {
  width: 100%;
  height: 100%;
  max-width: 200px;
  max-height: 200px;
  margin: 0 auto 20px auto;
  transform: rotate(-90deg);

  &-hole {
    fill: $black
  }

  &-ring {
    stroke: $light-gray;
  }

  &-segment {
    stroke: $secondary-color;
  }

}

text {
  color: $secondary-color;
  transform-origin: 21px 21px;
  transform: rotate(90deg);
  font-size: 12px;
  /* Réduisez la taille de la police selon vos préférences. */
  dy: 0.3em;
  /* Ajustement pour centrer verticalement le texte. */
}</style>
