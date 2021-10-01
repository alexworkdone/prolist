<template>
  <div class="container">
    <h1>Cписок</h1>
    <div class="m-b-24">
      {{ subtitle }}
    </div>

    <div v-if="!hideList" class="global-list">
      <row-list :row="titleList" num="№" class="table-header" />

      <template v-for="(item, index) in list">
        <row-list
          :row="item"
          :num="index + 1"
          :newRow="newRow"
          :colCount="colCount"
          :key="index"
        />
      </template>
    </div>
  </div>
</template>

<script>
import rowList from "@/components/RowList.vue";

export default {
  name: "Home",

  components: {
    rowList,
  },

  data: () => ({
    SpeechRecognition: null,
    subtitle: "",
    titleList: {
      name: "Имя продукта",
      count: "Количество",
    },
    list: [],
    tempRow: {
      name: "",
      count: "",
    },
    str: "",
    hideList: false,
    newRow: false,
    colCount: false,
  }),

  created() {
    this.checkIsDictionary();

    ["q", "w", "e", "r", "y"].map((item, index) => {
      let row = {
        name: item + index,
        count: index * 10,
      };
      this.list.push(row);
    });
  },

  methods: {
    checkIsDictionary() {
      if (
        window.SpeechRecognition ||
        window.webkitSpeechRecognition ||
        window.mozSpeechRecognition ||
        window.msSpeechRecognition
      ) {
        this.subtitle = "Браузер поддерживает данную технологию";
        this.recordVoice();
      } else {
        this.subtitle = "Не поддерживается данным браузером";
        this.hideList = true;
      }
    },

    startRecords() {
      this.SpeechRecognition.start();
    },

    recordVoice() {
      this.SpeechRecognition = new (window.SpeechRecognition ||
        window.webkitSpeechRecognition ||
        window.mozSpeechRecognition ||
        window.msSpeechRecognition)();

      this.SpeechRecognition.lang = "ru-RU";

      this.SpeechRecognition.onresult = (event) => {
        console.log(event.results[0][0].transcript);

        if (event.results[0][0].transcript === "новый ряд") {
          this.str = "";
          this.list.push(this.tempRow);
          this.newRow = true;
          this.colCount = false;
          return;
        }

        if (event.results[0][0].transcript === "количество") {
          this.str = "";
          this.colCount = true;
          this.newRow = false;
          return;
        }

        if (this.newRow) {
          this.str += `${event.results[0][0].transcript} `;
          this.list[this.list.length - 1].name = this.str;
        }

        if (this.colCount) {
          this.str += `${event.results[0][0].transcript} `;
          this.list[this.list.length - 1].count = this.str;
        }
      };

      this.SpeechRecognition.onend = () => {
        this.SpeechRecognition.start();
      };

      this.SpeechRecognition.start();
    },
  },
};
</script>

<style lang="scss">
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.container {
  margin: 0 auto;
  padding: 0 16px;
  max-width: 600px;
}
</style>
