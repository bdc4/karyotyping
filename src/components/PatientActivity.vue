<template>
  <div>

    <div>
      <div>
        <!--template :src="`../assets/patient${this.id}/conclusions/template.html`"></template-->
        
        <PatientAConclusions></PatientAConclusions>
      </div>
    </div>
    <v-snackbar v-model="popup.show" multi-line close-on-content-click :timeout="popup.timeout || -1">
      <v-row>
        <v-col cols="3" class="d-flex d-flex-row px-10" v-if="popup.images.length">
          <v-img class="activity-image" :src="popup.images[0]" max-width="60" max-height="100"></v-img>
          <v-img class="activity-image" :src="popup.images[1]" max-width="60" max-height="100"></v-img>
        </v-col>
        <v-col>
          {{ popup.message }}
        </v-col>
      </v-row>
      <v-row justify="center" v-if="!popup.correct">
        <v-btn class="my-5" @click="popup.show = false">Try Again</v-btn>
      </v-row>
    </v-snackbar>
    <v-card>
      <v-card-title>
        {{ activity.title }} {{ completion[id] ? '(Complete!)' : '' }}
      </v-card-title>
      <v-card-text v-if="!state.step.end">
        {{ activity.description }}
        Step: {{ stepIndex }}
        Key: {{ state.key }}
        <v-row class="pt-5">
          <v-col cols="1">
            <v-img :src="currentStepImage" @click="expandImage = true" class="activity-image" height="100">
              <v-dialog v-model="expandImage" activator="parent">
                <v-card title="Dialog">
                  <v-card-text>
                    <v-img :src="currentStepImage" height="100" class="activity-image"></v-img>
                  </v-card-text>
                </v-card>
              </v-dialog>
            </v-img>
          </v-col>
          <v-col cols="11"> {{ tooltip }} </v-col>

        </v-row>

      </v-card-text>

      <!-- Activity Completed -->
      <v-card-text v-else>



        <v-alert text color="success">{{ tooltip }}</v-alert>
        <v-btn @click="stepIndex = 0" color="secondary">Restart</v-btn>
      </v-card-text>
      <v-row class="pa-0 ma-0">
        <v-col v-for="(chromGroup, index) in images" :key="index" @click="selectAnswer(chromGroup, index)">
          <v-card width="110" height="150">
            <v-card-text>
              <v-row class="activity-card">
                <template v-for="chrom in chromGroup">
                  <v-img v-if="stepIndex == -1 || (!hiddenChroms.includes(chrom) && !chrom.includes('c'))" :key="chrom"
                    :cols="12 / chromGroup.length" :src="getImagePath(chrom)" height="100" max-width="60"
                    class="activity-image"></v-img>
                </template>
              </v-row>
              <v-row class="text-center">
                <v-col height="20">
                  <v-chip :color="(response[index + 1] || index + 1 == state.key) ? 'blue' : ''">
                    {{ (index == 22) ? 'XX/XY' : (index + 1) }}</v-chip>
                </v-col>
              </v-row>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
      <!--v-card-actions>
      <v-btn v-for="(action, index) in activity.actions" :key="index">{{ action.text }}</v-btn>
    </v-card-actions-->
    </v-card>
  </div>
</template>

<script>
import PatientData from '../assets/patients.json'
import PatientAConclusions from './PatientAConclusions.vue'
export default {
  name: "PatientActivity",
  components: {
    PatientAConclusions
  },
  data() {
    return {
      activityData: PatientData,
      defaultStepIndex: 0,
      popup: {
        message: '',
        images: [],
        show: false
      },
      completion: {},
      expandImage: false,
      conclusionComponent: null
    }
  },
  props: {
    id: String
  },
  computed: {
    activity() {
      return this.activityData[this.id]
    },
    stepIndex: {
      get() {
        return this.defaultStepIndex
      },
      set(newVal) {
        if (newVal < this.state.keys.length) {
          this.defaultStepIndex = newVal
        } else {
          alert(`Nice work! You've completed the activity for Patient ${this.id}!`)
          this.stepIndex = "-1";
          this.completion[this.id] = true;
        }
      }
    },
    state() {
      return {
        key: this.activity.data.keys[this.stepIndex],
        keys: this.activity.data.keys,
        step: this.activity.data.steps[this.stepIndex]
      }
    },
    currentChrom() {
      return (this.state.step && !this.state.step.end) ?
        (this.state.key + (this.state.step.target || '')) : undefined;
    },
    currentStepImage() {
      return this.currentChrom ? this.getImagePath(this.currentChrom) : undefined;
    },
    tooltip() {
      return this.state.step ? this.state.step.tooltip : undefined
    },
    hiddenChroms() {
      try {
        var list = [this.currentChrom];
        var responses = this.activity.data.responses[this.state.key];
        Object.keys(responses).forEach(key => {
          list.push(key + this.state.step.target);
        })
        return list
      } catch (e) {
        return []
      }
    },
    images() {
      var imageList = []
      // const addC = this.activity.data.addC || []
      for (var i = 1; i <= 23; i++) {
        var chrom = [];
        ['a', 'b', 'c'].forEach(letter => {
          var l = i.toString() + letter;
          try {
            this.getImagePath(l)
            chrom.push(l)
          } catch (e) {
            // stuff
            // console.log(`no matching ${letter} found for ${i}`)
          }
        })

        if (chrom.length == 0) {
          this.getImagePath(i.toString());
          chrom.push(i.toString())
        }



        //if (addC.includes(i)) {
        //  chrom.push((i.toString() + 'c'))
        //}
        imageList.push(chrom);
      }


      // console.log(imageList)
      return imageList;
    },
    spacers() {
      return [
        [-1, 0, 1, 2, -1, -1, 3, 4],
        [5, 6, 7, 8, -1, 9, 10, 11],
        [12, 13, 14, -1, 15, 16, 17, -1],
        [-1, 18, 19, -1, 20, 21, -1, 22]
      ]
    },
    response() {
      return this.state.key ? this.activity.data.responses[this.state.key] : {}
    }
  },
  methods: {
    async getConclusionComponent() {
      var component = await import(`./Patient${this.id}Conclusions.vue`)
      console.log(component.default)
      this.conclusionComponent = component.default;
    },
    getImagePath(img) {
      return require(`../assets/patient${this.id}/images/${img}.gif`)
    },
    selectAnswer(chromGroup, index) {
      if (chromGroup.includes(this.currentChrom)) {
        this.popup = {
          show: true,
          message: 'Nice work!',
          images: [],
          correct: true,
          timeout: 1000
        }
        this.stepIndex++;
      }
      else {
        var tip = this.response[index + 1];
        console.log(tip, this.activity.data.responses, this.state.key, index + 1)
        var images;
        try {
          images = [this.getImagePath((index + this.state.step.target + '')), this.currentStepImage]
        } catch (e) {
          images = [];
        }
        if (tip) {
          this.popup = {
            show: true,
            message: tip,
            images
          }
        }
      }
    }
  }
}
</script>

<style lang="scss">
.activity-image {
  .v-image__image--cover {
    background-size: auto !important;
  }
}

.activity-card {
  border-bottom: 1px solid black;
}
</style>