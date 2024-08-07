<script setup>
import { QuestionFilled } from "@element-plus/icons-vue";
import { ref } from "vue";

const ref1 = ref();
const selectedStrategy = ref(null);
const open = ref(false);

const selectStrategy = (strategy) => {
  selectedStrategy.value = strategy;
  updateStrategies();
};
const particlesLoaded = async (container) => {
  console.log("Particles container loaded", container);
};

const generalStrategies = ref([
  {
    title: "Hitman",
    description:
      "El primer enemigo que se vea es la Marca. No se puede plantar ni desactivar la spike hasta que la Marca haya sido eliminada.",
  },
  {
    title: "Secret Santa",
    description: "Ningún jugador puede comprar su propia arma.",
  },
  {
    title: "Moon Walk",
    description: "Los jugadores solo pueden moverse caminando hacia atrás.",
  },
  {
    title: "Solicito permiso",
    description:
      "Elige un jugador al azar. Este jugador se designa como el Oficial al mando. Los jugadores deben pedir y recibir el permiso verbal del Oficial antes de intercambiar armas, recargar o usar una habilidad.",
  },
  {
    title: "Armas Retornables",
    description:
      "Los jugadores no pueden recargar sus armas. Si un jugador vacía su cargador, debe detenerse y SOLTAR INMEDIATAMENTE el arma en el suelo. Sin embargo, pueden recoger armas que hayan sido descartadas de manera similar por otros jugadores.",
  },
  {
    title: "Media Naranja",
    description:
      "Los jugadores que disparen sus armas principales antes de plantar la spike no pueden dispararlas después. Los jugadores que usen habilidades antes de plantar la spike no pueden usarlas después.",
  },
  {
    title: "Shhh",
    description:
      "Tu equipo solo puede comprar armas con silenciador y nadie en el equipo puede hablar durante toda la ronda.",
  },
  {
    title: "El Coach",
    description:
      "El que esté al final del marcador de tu equipo es la única persona que puede usar su micrófono esta ronda. Debe intentar hacer calls para todos sus compañeros de equipo.",
  },
  {
    title: "Tu otra derecha",
    description:
      "Todos en tu equipo deben ponerse los auriculares al revés durante toda la ronda.",
  },
  {
    title: "Cañón de Cristal",
    description:
      "Cada compañero de equipo debe comprar el arma más cara que pueda pagar, pero no se les permite comprar armadura.",
  },
  {
    title: "CSGO",
    description:
      "Nadie en tu equipo puede usar habilidades durante esta ronda. Es como si estuvieran jugando CS.",
  },
  {
    title: "Trickshot",
    description:
      "Cada vez que te encuentres con un enemigo, debes hacer un giro de 360 grados antes de poder dispararle.",
  },
  {
    title: "Recogedor",
    description:
      "Cada vez que mates a un enemigo, debes recoger su arma y usarla para tu próxima baja. No puedes conseguir una baja con la misma arma más de una vez.",
  },
  {
    title: "Ahí viene Audaz",
    description:
      "Debes mantener presionada la tecla W durante toda la ronda y no puedes caminar (no shift).",
  },
  {
    title: "Doppelganger",
    description:
      "Si hay un enemigo en el otro equipo con el mismo agente que tú, debes ignorar a todos los demás enemigos hasta que hayas eliminado a tu doble.",
  },
  {
    title: "Cuchillos Afuera",
    description:
      "Solo se te permite moverte si estás sosteniendo tu cuchillo. Si deseas disparar, debes permanecer inmóvil y no puedes moverte hasta que vuelvas a sacar tu cuchillo.",
  },
  {
    title: "De Aguilita",
    description:
      "Todos en tu equipo deben jugar la ronda completa agachados, no pueden levantarse en ningún momento por ninguna razón.",
  },
  {
    title: "Concierto",
    description:
      "La primera persona que sea eliminada del equipo debe comenzar a cantar una canción, los demás que vayan siendo eliminados deben hacer los instrumentos o coros de la canción.",
  },
  {
    title: "El Viejo Oeste",
    description:
      "Todo tu equipo debe comprar solo Sheriffs. Se permite armadura, pero no otras armas. Puntos extra si puedes usar un acento Norteño o del Oeste durante la ronda.",
  },
  {
    title: "Fortnite",
    description: "Debes saltar cada vez que gires o te asomes a una esquina.",
  },
  {
    title: "Hijos de Odin",
    description:
      "Cada jugador debe comprar un Odin y atacar al equipo enemigo en grupo. Compra una Ares si no puedes permitirte un Odin. Compra una Frenzy si no puedes permitirte una Ares.",
  },
  {
    title: "Mi compa el Alucín",
    description:
      "Juega la ronda normalmente, sin embargo, no puedes usar calls normales. Preferiblemente usa calls que no existan en este mapa, calls de otros juegos/mapas. Sonar seguro es clave para esta estrategia.",
  },
  {
    title: "Cult of the Lamb",
    description:
      "Cuando el equipo haga la first kill, todo el equipo debe ir y rodear el cuerpo del enemigo y hacer un pequeño ritual.",
  },
  {
    title: "Muralla María",
    description: "Formen una pared horizontal y avancen juntos.",
  },
  {
    title: "Mmmm patas",
    description: "Solo puedes disparar a las piernas del enemigo.",
  },
  {
    title: "Spike Rush",
    description:
      "Todos los jugadores deben comprar todas sus habilidades y con el dinero restante todos deben comprar la misma arma.",
  },
  {
    title: "Voces del Más Allá",
    description:
      "Solo los jugadores que han sido eliminados pueden dar calls, usa preferiblemente una voz fantasmal.",
  },
  {
    title: "Piñata",
    description:
      "Todos los jugadores deben lanzar sus armas en un solo lugar del spawn formando una pila. Cuando la ronda comience, deben tomar un arma random de la pila.",
  },
  {
    title: "Susana Distancia",
    description:
      "No pueden haber dos jugadores en la misma zona de call del mapa.",
  },
  {
    title: "El Aguador",
    description:
      "Designa a un jugador del equipo para que este sea la única persona que pueda recargar las armas.",
  },
  {
    title: "Silencio Mortal",
    description: "Todos los jugadores deben poner el volumen del juego a 0.",
  },
]);

const attackerStrategies = ref([
  {
    title: "Full Fake",
    description:
      "Todos los jugadores deben tirar todas sus habilidades en un site y luego ir a plantar a otro site.",
  },
  {
    title: "Plant Fake",
    description:
      "Los jugadores deben Fakear el Planting de la spike en todos los sitios disponibles antes de plantarla definitivamente.",
  },
  {
    title: "Protejan al Presidente",
    description:
      "Designen a un jugador para ser el presidente, este solo podrá llevar la spike y comprar escudo, no puede disparar ni usar habilidades, los demás jugadores deben rodearlo y protejerlo por el resto de la ronda.",
  },
  {
    title: "Follow the leader",
    description:
      "Elijan a un jugador para ser el lider, todos deben de seguirlo en fila detrás de el, nadie puede separarse o salir de la linea.",
  },
  {
    title: "Speech Motivacional",
    description:
      "Elijan a un jugador para dar un speech motivacional al comenzar la ronda. Nadie puede salir del spawn hasta que haya terminado el discurso.",
  },
]);

const defenderStrategies = ref([
  {
    title: "Uno a la vez",
    description:
      "Solo un jugador puede salir del spawn a la vez, el resto del equipo debe hacer su mejor esfuerzo para esconderse en el spawn, solo puede salir otro jugador cuando el anterior sea eliminado.",
  },
  {
    title: "De cerca y Personal",
    description:
      "Todos deben comprar escopetas y holdear angulos cerrados dentro del site.",
  },
  {
    title: "Full Retake",
    description:
      "Todo el equipo debe permanecer en el spawn hasta que la spike sea plantada.",
  },
  {
    title: "Todo o Nada",
    description:
      "Todo el equipo debe ir a un site y defenderlo. Tienes 1/2 o 1/3 de probabilidad de elegir el site correcto, ¡Buena Suerte!",
  },
]);

const currentStrategies = ref([...generalStrategies.value]);
const lastStrategy = ref(null);

const updateStrategies = () => {
  switch (selectedStrategy.value) {
    case "atacante":
      currentStrategies.value = [
        ...generalStrategies.value,
        ...attackerStrategies.value,
      ];
      break;
    case "defensor":
      currentStrategies.value = [
        ...generalStrategies.value,
        ...defenderStrategies.value,
      ];
      break;
    default:
      currentStrategies.value = [...generalStrategies.value];
      break;
  }
  getRandomStrategy();
};

const getRandomStrategy = () => {
  let newStrategy = null;
  do {
    const randomIndex = Math.floor(
      Math.random() * currentStrategies.value.length
    );
    newStrategy = currentStrategies.value[randomIndex];
  } while (newStrategy === lastStrategy.value);
  lastStrategy.value = newStrategy;
  console.log(lastStrategy.value);
};

const options = ref({
  background: {
    color: {
      value: "#FF4656",
    },
  },
  fpsLimit: 60,
  interactivity: {
    events: {
      onClick: {
        enable: false,
        mode: "push",
      },
      onHover: {
        enable: true,
        mode: "repulse",
      },
    },
    modes: {
      bubble: {
        distance: 400,
        duration: 2,
        opacity: 0.8,
        size: 40,
      },
      push: {
        quantity: 4,
        duration: 5,
      },
      repulse: {
        distance: 200,
        duration: 0.4,
      },
    },
  },
  particles: {
    color: {
      value: "#ffffff",
    },
    links: {
      color: "#ffffff",
      distance: 150,
      enable: true,
      opacity: 0.5,
      width: 1,
    },
    move: {
      direction: "none",
      enable: true,
      outModes: "bounce",
      random: false,
      speed: 6,
      straight: false,
    },
    number: {
      density: {
        enable: true,
      },
      value: 150,
    },
    opacity: {
      value: 0.5,
    },
    shape: {
      type: "circle",
    },
    size: {
      value: { min: 1, max: 5 },
    },
  },
  detectRetina: true,
});
getRandomStrategy();
</script>

<template>
  <div class="container">
    <el-header class="navbar">
      <div class="navbar-left">
        <!-- SVG Inline -->
        <a
          href="https://linktr.ee/thejuker_gg"
          target="_blank"
          class="logo-link"
        >
          <svg
            id="ref2"
            class="logo"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 972.26 419.87"
          >
            <defs></defs>
            <path
              class="cls-1"
              d="m326.51,227.3l-.76,151.72-100.12,40.85-94.49-43.9.19-60.7-.19.76,38.49,20.23,59.06,14.32,16.61-10.12v-112.39l81.22-.76Z"
            />
            <path
              class="cls-1"
              d="m415.24,120.07l-.19,218.76,16.61,10.12,21.57-14.32V120.45l58.8-1.91v255.79l-77.31,43.9-77.31-40.85-.38-256.94,58.22-.38Z"
            />
            <path
              class="cls-1"
              d="m621.21,119.87l62.23-1.91-55.36,138.97,55.36,138.78-63.18-3.82-31.69-79.6.38,81.51-59.18.95V121.02l58.03-.38.38,82.27,33.02-83.04Z"
            />
            <path
              class="cls-1"
              d="m740.13,229.45l55.93-1.34v59.18l-55.55.57.19,47.15,55.55-1.34v59.18l-114.34,1.91V121.02l115.87-2.1-.95,58.98-56.88,1.91.19,49.63Z"
            />
            <path
              class="cls-1"
              d="m885.02,307.33l-11.26-.19v87.62h-56.89l-1.14-275.64,77.31-7.64,77.31,37.03,1.14,122.74-31.3,14.7,32.07,108.62-60.7,2.29-26.53-89.53Zm-10.5-62.04l16.61.57,21.57-16.23v-42.57l-16.61-12.03-21.57,2.86v67.38Z"
            />
            <path
              class="cls-1"
              d="m224.52,274.53c-21.46,0-38.85,21.32-38.85,47.61,0-26.3-17.39-47.61-38.85-47.61,21.46,0,38.85-21.32,38.85-47.61,0,26.3,17.39,47.61,38.85,47.61Z"
            />
            <path
              class="cls-1"
              d="m131.14,209.54s92.65,22.81,202.41,0v-25.66s-5.7-85.52-37.06-115.46h-2.85s4.28,47.04-14.25,66.99c0,0,5.7,29.93,2.85,32.78-2.85,2.85-21.38-78.4-115.46-142.54l-2.85,4.28s24.23,57.02,18.53,88.38c0,0,27.08,28.51,27.08,57.02,0,0-69.85-152.52-182.45,14.25l-2.85,4.28,2.85,2.85s76.97-76.97,104.06,12.83Z"
            />
            <circle class="cls-1" cx="155.37" cy="17.1" r="17.1" />
            <circle class="cls-1" cx="289.36" cy="54.17" r="17.1" />
            <circle class="cls-1" cx="17.1" cy="208.11" r="17.1" />
          </svg>
        </a>
      </div>
      <div class="navbar-center">Valorant Strat Roulette</div>
      <div class="navbar-right">
        <el-icon @click="open = true"><QuestionFilled /></el-icon>
      </div>
    </el-header>
    <el-main>
      <!-- Botones debajo del navbar -->
      <div class="button-container">
        <el-button
          ref="ref1"
          size="large"
          class="strategy-button attacker-button"
          :class="{
            'selected-attacker': selectedStrategy === 'atacante',
            'not-selected': selectedStrategy !== 'atacante',
          }"
          @click="selectStrategy('atacante')"
        >
          Atacante
        </el-button>
        <el-button
          size="large"
          class="strategy-button defender-button"
          :class="{
            'selected-defender': selectedStrategy === 'defensor',
            'not-selected': selectedStrategy !== 'defensor',
          }"
          @click="selectStrategy('defensor')"
        >
          Defensor
        </el-button>
      </div>
      <div class="particles-container">
        <vue-particles
          id="tsparticles"
          @particles-loaded="particlesLoaded"
          :options="options"
        />
      </div>
      <div class="card-container">
        <el-card
          shadow="always"
          :body-style="{
            padding: '30px',
            'font-size': '18px',
            height: '60%',
            display: 'flex',
            'flex-direction': 'column',
          }"
        >
          <template #header>
            <div class="card-header">
              <span>{{ lastStrategy.title }}</span>
            </div>
          </template>
          <!-- card body -->

          <div>{{ lastStrategy.description }}</div>
          <el-button
          id="stratButton"
            class="button-card"
            size="large"
            @click="getRandomStrategy()"
            >Nueva Estrategia</el-button
          >
        </el-card>
      </div>

      <el-tour v-model="open">
        <el-tour-step
          :target="ref1.$el"
          title="Selecciona tu lado"
          description="Elije si eres Atacante o Defensor para tener estreategias más específicas."
        >
        </el-tour-step>
        <el-tour-step
          target="#stratButton"
          title="Más estrategias!"
          description="Da clic en el botón para generar nuevas estrategias."
        />
        <el-tour-step
          target="#ref2"
          title="Visita mis redes"
          description="Puedes ver mis distintas redes para apoyarme cuando compartas este proyecto :)"
        />
      </el-tour>
    </el-main>
    <el-footer>
      <p>© 2024 The Juker</p>
    </el-footer>
  </div>
</template>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: white;
  padding: 0 20px;
  height: 80px;
  background-color: #111;
  border-bottom: 2px solid rgba(51, 51, 51, 0.25);
}

.navbar-left .logo {
  height: 50px;
  fill: #fff;
  cursor: pointer;
}

.navbar-center {
  font-size: 40px;
  font-weight: bold;
}

.navbar-right {
  display: flex;
  align-items: center;
}

.navbar-right .el-icon {
  font-size: 54px;
  cursor: pointer;
}
.navbar-left:hover .logo {
  fill: #7314bd;
}

.button-container {
  display: flex;
  justify-content: center;
  align-items: center; /* Centra verticalmente los botones */
  background-color: #17212b; /* Color de fondo del contenedor de botones */
  padding: 20px; /* Espaciado interno para separar los botones del borde del contenedor */
  height: 80px; /* Altura del contenedor de botones */
  gap: 40px; /* Espacio entre los botones */
}

.strategy-button {
  color: white;
  font-size: 23px; /* Aumenta el tamaño del texto */
  padding: 20px 35px; /* Aumenta el espaciado interno */
  transition: background-color 0.3s, border-color 0.3s;
  border: 1px solid transparent; /* Borde transparente por defecto */
}

.attacker-button {
  background-color: transparent; /* Fondo transparente por defecto para el botón de Atacante */
}

.defender-button {
  background-color: transparent; /* Fondo transparente por defecto para el botón de Defensor */
}

.strategy-button.selected-attacker {
  background-color: #ff4654; /* Color de fondo del botón seleccionado como Atacante */
}

.strategy-button.selected-defender {
  background-color: #455dff; /* Color de fondo del botón seleccionado como Defensor */
}

.strategy-button.not-selected {
  background-color: gray; /* Color de fondo para el botón no seleccionado */
}

.attacker-button:hover {
  background-color: #ff4654; /* Color de fondo al hacer hover en el botón de Atacante */
}

.defender-button:hover {
  background-color: #455dff; /* Color de fondo al hacer hover en el botón de Defensor */
}

.card-container {
  flex: 1; /* Hace que el contenedor del card ocupe el espacio restante */
  display: flex;
  align-items: center;
  justify-content: center;
}

.el-card {
  text-align: center;
  margin-top: 2rem;
  width: 100%;
  height: 350px;
  max-width: 700px;
  margin-left: 15px;
  margin-right: 15px;
}

.card-header {
  font-size: 30px;
}

.el-footer {
  background-color: #111;
  color: #fff;
  text-align: center;
  padding: 10px;
  margin: 0;
}

.container {
  display: flex;
  flex-direction: column;
  min-height: 100vh; /* Asegura que el contenedor ocupe toda la altura de la ventana */
}

.button-card {
  margin-top: auto;
  align-self: center;
  width: 40%;
  background-color: #000000;
  color: #fff;
  font-size: 15px;
  font-weight: bold;
}

.particles-container {
  position: relative;
  width: 100%;
  height: 100%;
  z-index: -1; /* Asegúrate de que el canvas de partículas esté en el fondo */
}

#tsparticles {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
