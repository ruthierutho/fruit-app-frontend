<template>
  <div>
    <h1>Fruits Of The World!</h1>
    <div>
      
      <fruits-list :fruits="fruits"></fruits-list>
     
      <modal name='fruit-modal' width="750" height="auto" :adaptive="true" :scrollable="true" :reset="true">
      <div class="pop-content">
      <button id="close" @click="hide()">x</button>
      <fruit-detail v-if="selectedFruit" :fruit="selectedFruit"></fruit-detail>
      <pie-chart v-if="selectedFruit" :options="pieOptions" :key="chartKey"></pie-chart>
      </div>
      </modal>
     
    </div>
  </div>
</template>

<script>
import { eventBus } from './main.js';

import FruitsList from './components/FruitsList.vue';
import FruitDetail from './components/FruitDetail.vue';
import FruitService from '@/services/FruitService';
import PieChart from "./components/PieChart.vue";

export default {
  name: "app",
  data(){
    return {
      chartKey: 0,
      fruits: [
    {
        "genus": "Malus",
        "name": "Apples",
        "emoji": "🍎",
        "family": "Rosaceae",
        "order": "Rosales",
        "origin": {
            "country": "Kazakhstan",
            "latitude": 48.0196,
            "longitude": 66.9237
        },
        "nutritions": {
            "carbohydrates": 11.4,
            "protein": 0.3,
            "fat": 0.4,
            "calories": 52,
            "sugar": 10.3
        }
    }, {
        "genus": "Prunus",
        "name": "Apricots",
        "emoji": "🍑",
        "family": "Rosaceae",
        "order": "Rosales",
        "origin": {
            "country": "China",
            "latitude": 35.8617,
            "longitude": 104.1954
        },
        "nutritions": {
            "carbohydrates": 3.9,
            "protein": 0.5,
            "fat": 0.1,
            "calories": 15,
            "sugar": 3.2
        }
    }, {
        "genus": "Musa",
        "name": "Bananas",
        "emoji": "🍌",
        "family": "Musaceae",
        "order": "Zingiberales",
        "origin": {
            "country": "Indonesia",
            "latitude": 0-0.7893,
            "longitude": 113.9213 
        },
        "nutritions": {
            "carbohydrates": 22,
            "protein": 1,
            "fat": 0.2,
            "calories": 96,
            "sugar": 17.2
        }
    }, {
        "genus": "Actinidia",
        "name": "Kiwis",
        "emoji": "🥝",
        "family": "Actinidiaceae",
        "order": "Ericales",
        "origin": {
            "country": "China",
            "latitude": 35.8617,
            "longitude": 104.1954
        },
        "nutritions": {
            "carbohydrates": 15,
            "protein": 1.1,
            "fat": 0.5,
            "calories": 61,
            "sugar": 9
        }
    }, {
        "genus": "Prunus",
        "name": "Cherries",
        "emoji": "🍒",
        "family": "Rosaceae",
        "order": "Rosales",
        "origin": {
            "country": "Turkey",
            "latitude": 38.9637,
            "longitude": 35.2433
        },
        "nutritions": {
            "carbohydrates": 12,
            "protein": 1,
            "fat": 0.3,
            "calories": 50,
            "sugar": 8
        }
    }, {
        "genus": "Citrus",
        "name": "Lemons",
        "emoji": "🍋",
        "family": "Rutaceae",
        "order": "Sapindales",
        "origin": {
            "country": "India",
            "latitude": 20.5937,
            "longitude": 78.9629
        },
        "nutritions": {
            "carbohydrates": 9,
            "protein": 1.1,
            "fat": 0.3,
            "calories": 29,
            "sugar": 2.5
        }
    }, {
        "genus": "Mangifera",
        "name": "Mangos",
        "emoji": "🥭",
        "family": "Anacardiaceae",
        "order": "Sapindales",
        "origin": {
            "country": "India",
            "latitude": 20.5937,
            "longitude": 78.9629
        },
        "nutritions": {
            "carbohydrates": 15,
            "protein": 0.82,
            "fat": 0.38,
            "calories": 60,
            "sugar": 13.7
        }
    }, {
        "genus": "Citrus",
        "name": "Oranges",
        "emoji": "🍊",
        "family": "Rutaceae",
        "order": "Sapindales",
        "origin": {
            "country": "China",
            "latitude": 35.8617,
            "longitude": 104.1954
        },
        "nutritions": {
            "carbohydrates": 8.3,
            "protein": 1,
            "fat": 0.2,
            "calories": 43,
            "sugar": 8.2
        }
    }, {
        "genus": "Pyrus",
        "name": "Pears",
        "emoji": "🍐",
        "family": "Rosaceae",
        "order": "Rosales",
        "origin": {
            "country": "China",
            "latitude": 35.8617,
            "longitude": 104.1954
        },
        "nutritions": {
            "carbohydrates": 15,
            "protein": 0.4,
            "fat": 0.1,
            "calories": 57,
            "sugar": 10
        }
    }, {
        "genus": "Ananas",
        "name": "Pineapples",
        "emoji": "🍍",
        "family": "Bromeliaceae",
        "order": "Poales",
        "origin": {
            "country": "Brazil",
            "latitude": 0-14.2350,
            "longitude": 0-51.9253
        },
        "nutritions": {
            "carbohydrates": 13.12,
            "protein": 0.54,
            "fat": 0.12,
            "calories": 50,
            "sugar": 9.85
        }
    }, {
        "genus": "Vitis",
        "name": "Grapes",
        "emoji": "🍇",
        "family": "Vitaceae",
        "order": "Vitales",
        "origin": {
            "country": "Greece",
            "latitude": 39.0742,
            "longitude": 21.8243
        },
        "nutritions": {
            "carbohydrates": 18.1,
            "protein": 0.7,
            "fat": 0.1,
            "calories": 69,
            "sugar": 15.5
        }
    }, {
        "genus": "Fragaria",
        "name": "Strawberries",
        "emoji": "🍓",
        "family": "Rosaceae",
        "order": "Rosales",
        "origin": {
            "country": "North America",
            "latitude": 54.5260,
            "longitude": 0-105.2551
        },
        "nutritions": {
            "carbohydrates": 5.5,
            "protein": 0.8,
            "fat": 0.4,
            "calories": 29,
            "sugar": 5.4
        }
    }, {
        "genus": "Solanum",
        "name": "Tomatoes",
        "emoji": "🍅",
        "family": "Solanaceae",
        "order": "Solanales",
        "origin": {
            "country": "The Andes Mountains",
            "latitude": 0-21.1608,
            "longitude": 0-66.7752
        },
        "nutritions": {
            "carbohydrates": 3.9,
            "protein": 0.9,
            "fat": 0.2,
            "calories": 74,
            "sugar": 2.6
        }
    }, {
        "genus": "Citrullus",
        "name": "Watermelon",
        "emoji": "🍉",
        "family": "Cucurbitaceae",
        "order": "Cucurbitales",
        "origin": {
            "country": "South Africa",
            "latitude": 0-30.5595,
            "longitude": 22.9375
        },
        "nutritions": {
            "carbohydrates": 8,
            "protein": 0.6,
            "fat": 0.2,
            "calories": 30,
            "sugar": 6
        }
    },
    {
        "genus": "Persea",
        "name": "Avocados",
        "emoji": "🥑",
        "family": "Lauraceae",
        "order": "Laurales",
        "origin": {
            "country": "Mexico",
            "latitude": 23.6260,
            "longitude": 0-102.5375
        },
        "nutritions": {
            "carbohydrates": 8.5,
            "protein": 2,
            "fat": 15,
            "calories": 160,
            "sugar": 0.7
        }
    }
],
      selectedFruit: null,

      pieOptions: {
        chart: {
          type: "pie",
          options3d: {
          enabled: true,
          alpha: 45
          }
        },
        title: {
        text: "Relative proportions:"
        },
        subtitle: {
        text: "carboydrates, fat and protein (per 100g)"
        },
        plotOptions: {
          pie: {
            allowPointSelect: true,
            cursor: 'pointer',
            dataLabels: {
                enabled: true,
                format: '<b>{point.name}</b>: {point.percentage:.1f} %'
            }
          }
        },
        series: [
          {
            type: 'pie',
            name: 'Amount in grams',
            keys: ['name', 'y', 'sliced', 'selected'],
            data: []
          }
        ]
      } 
    }
  },
  mounted(){
    // this.fetchFruits();

    eventBus.$on('fruit-selected', (fruit) => {
      this.selectedFruit = fruit
      this.updateFruitData()
      this.show()
    })


  },
  methods: {
    // fetchFruits() {
    //   FruitService.getFruits()
    //     .then(fruits => this.fruits = fruits);
    // },
    show () {
      this.$modal.show('fruit-modal');
    },
    hide () {
      this.$modal.hide('fruit-modal');
    },
    updateFruitData() {
      const updatedData = [['Carbohydrates', this.selectedFruit.nutritions.carbohydrates],
            ['Fat', this.selectedFruit.nutritions.fat],
            ['Protein', this.selectedFruit.nutritions.protein]]
            this.pieOptions.series[0].data = updatedData
            this.chartKey += 1
            // Update key to force re-render
    }
  },
  components: {
    "fruits-list": FruitsList,
    "fruit-detail": FruitDetail,
    
    "pie-chart": PieChart
  }
}
</script>

<style>


div > h1 {
  
    font-family: 'Montserrat', sans-serif;
    font-size: 60pt;
    width: 85%;
    border: 1px;
    background-color: rgb(253, 243, 129);
    padding: 20px;
    margin: 10px;
    margin-left: 70px;
    margin-right: 70px;
    text-align: center;
    border-radius: 5px;
    
    
    color: rgb(255, 153, 0);
    
    box-shadow: 5px 10px 5px orange;
}

#close {
  font-family: 'Montserrat', sans-serif;
  background-color:rgba(253, 243, 129, 0.961);
  color: rgb(255, 153, 0);
  border-block-color: rgb(255, 153, 0);
  border-radius: 5px;
  border: 0px;
  font-size: 35px;
  text-emphasis: bold;
  margin-left: 700px;
  padding-top: 0px;
  padding-bottom: 0px;
}

#close:hover {
  color: rgb(255, 184, 4);
}

.pop-content {
  overflow-y: auto;
  height: 100%;
  background-color: rgba(253, 243, 129, 0.906);
}

body {
  background: url('./assets/background_berries.jpg');
  height: 25%;
  background-position: center;
  background-repeat: repeat;
  /* background-size: cover; */
}

</style>
