<template>
  <div v-if="playerStats">
    <div class="player">
      <div class="player__inner">
        <CardsHeaderCards :playerData="playerData"/>
        <div class="player-stats">
          <div class="test">
            <div>
              <div class="player-stats__kd">
                <p>Ratio K/D: </p>
                <p><strong>{{ playerStats.lifetime["Average K/D Ratio"] }}</strong></p>
              </div>
              <div class="player-stats__recent-results">
                <div class="title">Résultats récents: </div>
                <div class="results__forme">
                  <div v-for="(result, index) in props.playerStats.lifetime['Recent Results']" :key="index">
                    <span v-if="result === '1'">✅</span>
                    <span v-else-if="result === '0'">❌</span>
                  </div>
                </div>
              </div>
            </div>
            <div class="player-stats__winrate">
              <WidgetsGraphCirc display="% de victoire" :value="props.playerStats.lifetime['Win Rate %']" />
              <WidgetsGraphCirc display="% de headshot" :value="props.playerStats.lifetime['Average Headshots %']" />
            </div>

          </div>

          <div class="player-stats__bestMap">
            Meilleurs maps :
            <div class="player-stats__carousel" @mousedown="startDrag" @mouseleave="stopDrag" @mouseup="stopDrag"
              @mousemove="moveDrag" @wheel="handleWheel">
              <div class="player-stats__best-maps">
                <div v-for="segment in bestMaps" :key="segment.label" class="player-stats__map">
                  <img :src="segment.img_regular" alt="Image de la carte">
                  <div class="player-stats__best-maps-stats">
                    <div>K/D: <span class="value">{{ segment.stats["Average K/D Ratio"] }}</span></div>
                    <div>MJ: <span class="value">{{ segment.stats.Matches }}</span></div>
                  </div>
                  <WidgetsGraphBar :value="segment.stats['Average Headshots %']" text="% HS:" />
                  <WidgetsGraphBar :value="segment.stats['Win Rate %']" text="% Victoire:" />
                </div>
              </div>
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
}

// Vous n'avez plus besoin d'utiliser `.value` avec `playerStats` car il n'est pas un `ref`.
const bestMaps = computed(() => {
  if (props.playerStats && props.playerStats.segments) {
    return props.playerStats.segments.sort((a, b) => parseFloat(b.stats["Win Rate %"]) - parseFloat(a.stats["Win Rate %"])).slice(0, 3);
  }
  return [];
});

// Carrousel
const isDragging = ref(false);
let startX;
let scrollLeft;

onMounted(() => {
  document.addEventListener('mousemove', moveDrag);
  document.addEventListener('mouseup', stopDrag);
});

onUnmounted(() => {
  document.removeEventListener('mousemove', moveDrag);
  document.removeEventListener('mouseup', stopDrag);
});

const preventDefaultScroll = (e) => e.preventDefault();

const startDrag = (e) => {
  isDragging.value = true;
  startX = e.pageX - e.currentTarget.offsetLeft; // utilisez currentTarget pour cibler l'élément sur lequel l'événement a été enregistré
  scrollLeft = e.currentTarget.scrollLeft;
  e.currentTarget.classList.add('is-grabbing');

  document.addEventListener('touchmove', preventDefaultScroll, { passive: false });
  document.addEventListener('wheel', preventDefaultScroll, { passive: false });
};

const stopDrag = (e) => {
  isDragging.value = false;
  e.currentTarget.closest('.player-stats__carousel').classList.remove('is-grabbing');

  document.removeEventListener('touchmove', preventDefaultScroll);
  document.removeEventListener('wheel', preventDefaultScroll);
};

const moveDrag = (e) => {
  if (!isDragging.value) return;
  e.preventDefault(); // Empêche le défilement
  const target = document.querySelector('.player-stats__carousel');
  const x = e.pageX - target.offsetLeft;
  const walk = (x - startX) * 2; // multipliez par un facteur pour augmenter la vitesse de défilement
  target.scrollLeft = scrollLeft - walk;

};




const handleWheel = (e: WheelEvent) => {
  const target = e.currentTarget as HTMLElement;
  target.scrollLeft += e.deltaY * 1;
  document.addEventListener('touchmove', preventDefaultScroll, { passive: false });
  document.addEventListener('wheel', preventDefaultScroll, { passive: false });

};



const handleGlobalMouseDown = (event) => {
  if (event.target.closest('.player-stats__carousel')) {
    document.body.style.overflow = 'hidden';
  }
}

const handleGlobalMouseUp = () => {
  document.body.style.overflow = 'auto';
}

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

  .player-stats__bestMap {
    color: $white;
    margin: $font-size-xl;

    .player-stats__carousel {
      padding-top: $spacing-m;
      overflow-x: scroll;
      white-space: nowrap;
      width: 100%;
      cursor: grab;

      &.is-grabbing {
        cursor: grabbing;
      }

      &::-webkit-scrollbar {
        display: none; // cacher la barre de défilement pour les navigateurs WebKit
      }
    }

    .player-stats__best-maps {
      display: inline-block;

      &-stats {
        display: flex;
        justify-content: space-between;
        color: $white;

        .value {
          color: $main-color;
        }
      }
    }

    .player-stats__map {
      display: inline-block;
      vertical-align: top;
      width: auto; // laissez le navigateur définir la largeur
      margin: 0 10px; // ajustez la marge selon vos besoins
    }

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
}

.player-stats__winrate{
  display: flex;
  flex-direction: row;
  margin-top: $spacing-m;
}
</style>
