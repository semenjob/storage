<template>
  <div class="telephone-app">onli telephone 412px</div>
  <h1>Intertop APP</h1>
  <input
    @input="filterArticle()"
    class="searchInput"
    id="search"
    v-model="searchArticle"
    autocomplete="off"
  />
  <div class="text">Введите названиме бренда, например 'ECCO'</div>
  <div v-if="filteredArticles.length < 4">
    <ul
      class="filtersList"
      v-for="filteredArticles in filteredArticles"
      :key="filteredArticles"
      @:click="autocompletePushToInput(filteredArticles)"
    >
      {{
        filteredArticles
      }}
    </ul>
  </div>
  <button
    class="search_btn btn"
    @:click="searchBrandName(searchArticle.toLowerCase())"
  >
    Search
  </button>
  <div class="infoStage">
    <div class="red">
      Stage 1
      <div class="color color-red"></div>
    </div>
    <div class="green">
      Stage 2
      <div class="color"></div>
    </div>
  </div>
  <div v-if="1" class="storage">
    <img src="./storageplan/storage.jpg" alt="storage" />
    <div
      v-for="articleName in sel.articlePosition"
      :key="articleName.name"
      :class="{
        'stage-2': articleName.stage == '2',
      }"
      :style="{
        top: `${articleName.x}px`,
        left: `${articleName.y}px`,
      }"
      class="cordinate_article"
    >
      {{ articleName.articleName }}
    </div>
  </div>
</template>

<script>
export default {
  name: "app",

  data() {
    return {
      sel: "",
      searchArticle: "",
      storageArticles: [
        {
          article: "panama jack",
          articlePosition: [
            { articleName: "pw", stage: "1", x: "440", y: "140" },
            // { articleName: "zw", stage: "1", x: "250", y: "180" },
          ],
        },
        {
          article: "gunter",
          articlePosition: [
            { articleName: "gr", stage: "1", x: "500", y: "180" },
          ],
        },
        {
          article: "ecco",
          articlePosition: [
            { articleName: "zm", stage: "1", x: "150", y: "80" },
            { articleName: "zw", stage: "1", x: "250", y: "180" },
            { articleName: "zk", stage: "1", x: "150", y: "100" },
          ],
        },
        {
          article: "garvalin",
          articlePosition: [
            { articleName: "gl", stage: "1", x: "440", y: "140" },
          ],
        },
        {
          article: "tnf",
          articlePosition: [
            { articleName: "no", stage: "2", x: "300", y: "50" },
            { articleName: "nv", stage: "2", x: "340", y: "180" },
            { articleName: "nt", stage: "2", x: "70", y: "220" },
          ],
        },
        {
          article: "braska",
          articlePosition: [
            { articleName: "bs", stage: "1", x: "300", y: "280" },
            { articleName: "br", stage: "1", x: "300", y: "50" },
            { articleName: "yz", stage: "1", x: "10", y: "120" },
            { articleName: "2s", stage: "2", x: "10", y: "120" },
          ],
        },
        {
          article: "sketchers",
          articlePosition: [
            { articleName: "kk", stage: "1", x: "170", y: "10" },
            { articleName: "km", stage: "2", x: "220", y: "10" },
            { articleName: "kw", stage: "1", x: "230", y: "320" },
          ],
        },
        {
          article: "adidas",
          articlePosition: [
            { articleName: "cn", stage: "2", x: "220", y: "330" },
            { articleName: "cp", stage: "2", x: "70", y: "100" },
          ],
        },
        {
          article: "puma",
          articlePosition: [
            { articleName: "cj", stage: "2", x: "350", y: "80" },
            // { articleName: "ci", stage: "2", x: "100", y: "100" },
            { articleName: "ck", stage: "2", x: "10", y: "20" },
            // { articleName: "cl", x: "200", y: "200" },
          ],
        },
        {
          article: "tomy helfigger",
          articlePosition: [
            { articleName: "td", stage: "2", x: "570", y: "250" },
            { articleName: "te", stage: "2", x: "170", y: "250" },
          ],
        },
        {
          article: "lacosta",
          articlePosition: [
            { articleName: "ll", stage: "2", x: "10", y: "130" },
            { articleName: "lk", stage: "2", x: "250", y: "250" },
          ],
        },
        {
          article: "vagabond",
          articlePosition: [
            { articleName: "vw", stage: "2", x: "450", y: "250" },
          ],
        },
        {
          article: "m wone",
          articlePosition: [
            { articleName: "oi", stage: "2", x: "450", y: "290" },
            { articleName: "8l", stage: "2", x: "220", y: "50" },
            { articleName: "8k", stage: "2", x: "120", y: "50" },
          ],
        },
        {
          article: "rispetto",
          articlePosition: [
            { articleName: "rpt", stage: "2", x: "300", y: "290" },
          ],
        },
        {
          article: "convers",
          articlePosition: [
            { articleName: "ca", stage: "2", x: "170", y: "80" },
            { articleName: "cb", stage: "2", x: "570", y: "110" },
          ],
        },
        {
          article: "hogl",
          articlePosition: [
            { articleName: "yn", stage: "2", x: "450", y: "250" },
          ],
        },
        {
          article: "imac",
          articlePosition: [
            { articleName: "yh", stage: "2", x: "280", y: "180" },
          ],
        },
        {
          article: "ikos",
          articlePosition: [
            { articleName: "gl", stage: "1", x: "170", y: "250" },
          ],
        },
        {
          article: "camper",
          articlePosition: [
            { articleName: "aw", stage: "1", x: "80", y: "140" },
            { articleName: "am", stage: "1", x: "80", y: "50" },
            { articleName: "an", stage: "1", x: "70", y: "220" },
          ],
        },
        {
          article: "caprice",
          articlePosition: [
            { articleName: "eo", stage: "1", x: "150", y: "80" },
          ],
        },
        {
          article: "clarks",
          articlePosition: [
            { articleName: "om", stage: "1", x: "450", y: "210" },
            { articleName: "ow", stage: "1", x: "220", y: "210" },
            { articleName: "ok", stage: "2", x: "70", y: "100" },
          ],
        },
        {
          article: "geox",
          articlePosition: [
            { articleName: "xm", stage: "1", x: "200", y: "140" },
            { articleName: "xw", stage: "2", x: "470", y: "100" },
            { articleName: "xk", stage: "2", x: "470", y: "140" },
          ],
        },
        {
          article: "hoka",
          articlePosition: [
            { articleName: "hkb", stage: "2", x: "350", y: "290" },
            { articleName: "hka", stage: "2", x: "350", y: "180" },
          ],
        },
        {
          article: "ricker",
          articlePosition: [
            { articleName: "rw", stage: "2", x: "200", y: "140" },
            { articleName: "rk", stage: "2", x: "200", y: "210" },
          ],
        },
        {
          article: "bagatt",
          articlePosition: [
            { articleName: "bat", stage: "1", x: "470", y: "210" },
          ],
        },
        {
          article: "emu",
          articlePosition: [
            { articleName: "yk", stage: "1", x: "470", y: "210" },
          ],
        },
        {
          article: "tamaris",
          articlePosition: [
            { articleName: "is", stage: "2", x: "200", y: "100" },
          ],
        },
        {
          article: "calvin klein",
          articlePosition: [
            { articleName: "skm", stage: "1", x: "430", y: "140" },
            { articleName: "skw", stage: "1", x: "470", y: "140" },
          ],
        },

        {
          article: "timberland",
          articlePosition: [
            { articleName: "tf", stage: "1", x: "450", y: "100" },
            { articleName: "tl", stage: "1", x: "250", y: "100" },
            { articleName: "tg", stage: "1", x: "200", y: "140" },
          ],
        },
        {
          article: "vans",
          articlePosition: [
            { articleName: "v", stage: "1", x: "430", y: "180" },
            { articleName: "vz", stage: "1", x: "250", y: "250" },
            { articleName: "vx", stage: "1", x: "70", y: "230" },
            { articleName: "aw", stage: "1", x: "70", y: "100" },
          ],
        },
        {
          article: "remonte",
          articlePosition: [
            { articleName: "rd", stage: "1", x: "500", y: "180" },
          ],
        },
        {
          article: "pikolonos",
          articlePosition: [
            { articleName: "sd", stage: "2", x: "570", y: "250" },
            { articleName: "sh", stage: "2", x: "100", y: "80" },
          ],
        },
        {
          article: "nike",
          articlePosition: [
            { articleName: "ce", stage: "2", x: "570", y: "60" },
            { articleName: "cf", stage: "2", x: "230", y: "180" },
            { articleName: "cg", stage: "2", x: "470", y: "210" },
          ],
        },
        {
          article: "new balance",
          articlePosition: [
            { articleName: "mq", stage: "2", x: "180", y: "170" },
            // { articleName: "mj", stage: "2", x: "-", y: "-" },
            // { articleName: "mg", stage: "2", x: "1", y: "1" },
            { articleName: "mu", stage: "2", x: "460", y: "250" },
          ],
        },
        {
          article: "guess",
          articlePosition: [
            { articleName: "7h", stage: "1", x: "30", y: "10" },
          ],
        },
        {
          article: "filip shuze",
          articlePosition: [
            { articleName: "3h", stage: "2", x: "500", y: "180" },
          ],
        },
        {
          article: "marco tozzi",
          articlePosition: [
            { articleName: "3h", stage: "2", x: "100", y: "50" },
          ],
        },
        {
          article: "bugatti",
          articlePosition: [
            { articleName: "yd", stage: "2", x: "10", y: "100" },
            { articleName: "ye", stage: "2", x: "70", y: "230" },
          ],
        },
        {
          article: "asics",
          articlePosition: [
            { articleName: "6d", stage: "2", x: "150", y: "330" },
            { articleName: "6c", stage: "2", x: "450", y: "330" },
            // { articleName: "6b", stage: "2", x: "-", y: "-" },
          ],
        },
        {
          article: "kids",
          articlePosition: [
            { articleName: "kd", stage: "2", x: "480", y: "330" },
            // { articleName: "6b", stage: "2", x: "-", y: "-" },
          ],
        },
        {
          article: "betsy",
          articlePosition: [
            { articleName: "0n", stage: "1", x: "500", y: "180" },
            { articleName: "8r", stage: "1", x: "470", y: "180" },
          ],
        },
        {
          article: "armani exchange",
          articlePosition: [
            { articleName: "wh", stage: "2", x: "-", y: "-" },
            { articleName: "wd", stage: "2", x: "570", y: "250" },
          ],
        },
        //-not ava-able
        {
          article: "bronx",
          articlePosition: [
            { articleName: "bx", stage: "2", x: "50", y: "50" },
          ],
        },
        {
          article: "marko polo",
          articlePosition: [
            { articleName: "po", stage: "1", x: "50", y: "50" },
            // { articleName: "zw", x: "100", y: "100" },
          ],
        },
        {
          article: "ea7",
          articlePosition: [
            { articleName: "-", stage: "-", x: "-", y: "-" },
            { articleName: "-", stage: "-", x: "-", y: "-" },
            { articleName: "-", stage: "-", x: "-", y: "-" },
          ],
        },
        {
          article: "columbia",
          articlePosition: [
            { articleName: "-", stage: "-", x: "-", y: "-" },
            { articleName: "-", stage: "-", x: "-", y: "-" },
            { articleName: "-", stage: "-", x: "-", y: "-" },
          ],
        },
        {
          article: "buffalo",
          articlePosition: [
            { articleName: "-", stage: "-", x: "-", y: "-" },
            { articleName: "-", stage: "-", x: "-", y: "-" },
            { articleName: "-", stage: "-", x: "-", y: "-" },
          ],
        },
        {
          article: "napapijri ",
          articlePosition: [
            { articleName: "-", stage: "-", x: "-", y: "-" },
            { articleName: "-", stage: "-", x: "-", y: "-" },
            { articleName: "-", stage: "-", x: "-", y: "-" },
          ],
        },
      ],
      filteredArticles: [],
    };
  },

  methods: {
    searchBrandName(art) {
      this.sel = this.storageArticles.find((a) => a.article === art);
      this.searchArticle = "";
    },

    autocompletePushToInput(brand) {
      this.searchArticle = brand;
    },

    filterArticle() {
      this.filteredArticles = this.storageArticles
        .map((art) => art.article)
        .filter((art) => {
          return art.toLowerCase().startsWith(this.searchArticle.toLowerCase());
        });
    },
  },
};
</script>

<style src="./style.css"></style>
