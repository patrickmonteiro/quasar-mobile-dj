<template>
  <q-page class="container">
    <div class="row">
      <div class="col-12 q-pt-sm q-pl-sm">
        <!-- <div class="song" >
          <button data-id_track="1" class="play play-1">Play</button>
          <audio onended="stopTrack(1)" class="track-1" src="http://kiki.tout.mou.free.fr/zic/14-ian_pooley-chord_memory_(daft_punk_remix).mp3" controls preload="auto" autobuffer></audio>
        </div> -->
        <div class="row">
          <div class="col-6">
            <div class="vinyl vinyl-1" :class="play1 ? 'play' : 'pause'">
              <div class="grooves"></div>
              <div class="light"></div>
              <div class="light-alt"></div>
              <div class="macaron">
                <img class="cover" src="statics/app-logo-128x128.png" alt="">
              </div>
            </div>
            <q-btn @click="playMusic()">
              Play
            </q-btn>
            <q-btn @click="stopMusic()">
              Stop
            </q-btn>
            <q-media-player
              v-show="false"
              type="audio"
              :sources="sources"
              :volume="volume1"
              ref="play1"
            />
          </div>
          <div class="col-6">
            <div class="vinyl vinyl-1" :class="play2 ? 'play' : 'pause'">
              <div class="grooves"></div>
              <div class="light"></div>
              <div class="light-alt"></div>
              <div class="macaron">
                <img class="cover" src="statics/app-logo-128x128.png" alt="">
              </div>
            </div>
            <q-btn @click="playMusic2()">
              Play
            </q-btn>
            <q-btn @click="stopMusic2()">
              Stop
            </q-btn>
            <!-- <q-slider
              v-model="volume2"
              :min="0"
              :max="100"
              snap
              label
              label-always
              color="purple"/> -->
            <q-media-player
              v-show="false"
              type="audio"
              :sources="sources2"
              :volume="volume2"
              ref="play2"
            />
          </div>
        </div>
        <div class="row justify-center">
          <div class="col-10">
             <q-slider
              v-model="volume"
              :min="-100"
              :max="100"
              snap
              label
              label-always
              color="purple"/>
          </div>
        </div>

      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      volume: -100,
      play1: false,
      volume1: 50,
      play2: false,
      volume2: 0,
      sources: [
        {
          src: 'https://raw.githubusercontent.com/quasarframework/quasar-ui-qmediaplayer/dev/demo/src/statics/media/Scott_Holmes_-_04_-_Upbeat_Party.mp3',
          type: 'audio/mp3'
        }
      ],
      sources2: [
        {
          src: 'statics/corazon.mp3',
          type: 'audio/mp3'
        }
      ]
    }
  },
  watch: {
    volume: function (val) {
      if (val < 0) {
        console.log(val)
        this.volume1 = (val * -1)
        this.volume2 = 0
      } else {
        this.volume1 = 0
        this.volume2 = val
      }
    }
  },
  methods: {
    playMusic () {
      this.play1 = true
      this.$refs.play1.play()
    },
    stopMusic () {
      this.play1 = false
      this.$refs.play1.pause()
    },
    playMusic2 () {
      this.play2 = true
      this.$refs.play2.play()
    },
    stopMusic2 () {
      this.play2 = false
      this.$refs.play2.pause()
    }
  }
}
</script>

<style scoped>
.vinyl {
  position: relative;
  display: inline-block;
  /* margin: 50px 50px 0; */
  width: 10rem;
  height: 10rem;
  border-radius: 50%;
  background-color: #040504;
  box-shadow: 1px 1px 10px #000;
}

.light,
.light-alt {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 5;
  border-radius: 50%;
  animation: reflection 20s infinite ease-in-out;
}

.light {
  background-image: linear-gradient(50deg, transparent, rgba(63, 62, 62, 0.3), transparent);
}

.light-alt {
  background-image: linear-gradient(-160deg, transparent 40%, rgba(255, 255, 255, 0.1) 50%, transparent 60%);
}

.macaron {
  position: absolute;
  top: 50%;
  left: 50%;
  z-index: 10;
  margin: -16% 0 0 -16%;
  width: 33.33%;
  height: 33.33%;
  border-radius: 50%;
}
.macaron .cover {
  width: 100%;
  height: 100%;
  border-radius: 50%;
}
.macaron:after {
  position: absolute;
  top: 50%;
  left: 50%;
  z-index: 6;
  display: block;
  margin: -4% 0 0 -4%;
  width: 8%;
  height: 8%;
  border-radius: 50%;
  background: white;
  box-shadow: inset 0 0 2px #000;
  content: "";
}

.grooves {
  position: absolute;
  top: 2%;
  right: 2%;
  bottom: 2%;
  left: 2%;
  z-index: 5;
  border-radius: 50%;
  background-image: radial-gradient(center center, circle closest-side, transparent 43%, transparent 53%, #000 54%, transparent 54%, transparent 64%, #000 65%, transparent 65%, transparent 75%, #000 76%, transparent 76%, transparent 86%, #000 87%, transparent 87%, transparent 97%, #000 98%, transparent 98%);
  background-image: -webkit-radial-gradient(center center, circle closest-side, transparent 43%, transparent 53%, #000 54%, transparent 54%, transparent 64%, #000 65%, transparent 65%, transparent 75%, #000 76%, transparent 76%, transparent 86%, #000 87%, transparent 87%, transparent 97%, #000 98%, transparent 98%);
}

.play .macaron,
.play .grooves,
.play .macaron .cover {
  animation: rotation 4s infinite linear;
}

.paused .macaron,
.paused .grooves,
.paused .macaron .cover {
  animation-play-state: paused;
}

.vinyl-picture-disc .macaron {
  top: 0%;
  left: 0%;
  z-index: 4;
  margin: 0;
  width: 100%;
  height: 100%;
}
.vinyl-picture-disc .macaron:after {
  margin: -1.25% 0 0 -1.25%;
  width: 2.5%;
  height: 2.5%;
  background: white;
}

.song {
  display: block;
  margin: 50px 50px 0;
  width: 400px;
  text-align: center;
}
.song audio {
  display: none;
}

@keyframes rotation {
  0% {
    transform: rotate(0);
  }
  100% {
    transform: rotate(360deg);
  }
}
@keyframes reflection {
  0% {
    filter: blur(5px);
    transform: rotate(0);
  }
  25% {
    transform: rotate(5deg);
  }
  50% {
    filter: blur(10px);
    transform: rotate(0);
  }
  75% {
    transform: rotate(-5deg);
  }
  100% {
    filter: blur(5px);
    transform: rotate(0);
  }
}

</style>
