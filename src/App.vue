<script setup>
import { ref } from 'vue';

const downloadDelay = ref(0)
const downloadLink = ref('')
const downloadQuery = ref(false)
const downloadTarget = ref(false)
const downloadCount = ref(1)

async function handleDownload() {
  for (let i = 0; i < downloadCount.value; i++) {
    await new Promise(resolve => setTimeout(resolve, downloadDelay.value));

    const downloadElement = document.createElement('a');
    downloadElement.href = downloadQuery.value ? `${downloadLink.value}?${i}` : downloadLink.value;
    if(downloadTarget.value === true) {
      downloadElement.target = '_blank'
    }
    document.body.appendChild(downloadElement);
    downloadElement.click();
    document.body.removeChild(downloadElement);
  }
}
</script>

<template>
  <h1>檔案下載測試</h1>
  <div>
    <a href="/">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="/">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <div style="display: flex; justify-content: space-evenly;">
    <button @click="handleDownload">自動下載</button>
    <button>
      <template v-if="downloadTarget">
        <a style="color:black" :href="downloadLink" target="_blank">手動下載</a>
      </template>
      <template v-else>
        <a style="color:black" :href="downloadLink">手動下載</a>
      </template>
    </button>
  </div>
 
  <hr>

  <h2>下載設定</h2>
  <div class="wrapper">
    <div>下載連結：</div>
    <input v-model="downloadLink" type="text" />
  </div>
  <div class="wrapper">
    <div>下載使用 target blank：</div>
    <input v-model="downloadTarget" type="checkbox" />
  </div>

  <hr>

  <h2>自動下載設定</h2>
  <div class="wrapper">
    <div>下載延遲：</div>
    <input v-model="downloadDelay" type="text" />
  </div>
  <div class="wrapper">
    <div>下載次數：</div>
    <input v-model="downloadCount" type="text" />
  </div>
  <div class="wrapper">
    <div>下載使用 query string：</div>
    <input v-model="downloadQuery" type="checkbox" />
  </div>

  <!-- <hr> -->

  <!-- <h2>其他</h2>
  <button>
    <a href="chrome://settings/privacy" target="_blank">開啟 Chrome 權限設定</a>
  </button> -->
</template>

<style scoped>
hr {
  margin: 30px 0;
}
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}

.wrapper {
  display:flex;
  justify-content: space-between;
  margin:20px 0;
}

.wrapper > input{
  margin-left: 100px;
}
</style>
