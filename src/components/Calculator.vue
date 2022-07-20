<template>
  <div class="form">
    <input
      type="text"
      v-model="key"
      placeholder="Enter your key"
      @change="cal()"
    />
    <div class="keyList" v-if="!isNaN(key)">
      <ul>
        <li v-for="(k, index) in keyList" :key="index">
          <p class="no">ข้อ {{ index + 1 }}</p>
          <p class="key">
            {{ k }}
          </p>
        </li>
      </ul>
    </div>
    <input
      placeholder="Enter student answer"
      type="text"
      v-model="answer"
      @click="answer = ''"
      @change="cal()"
    />
    <p class="detail btn" @click="showDetail = !showDetail">
      แสดง/ซ่อนรายละเอียด
    </p>
    <div
      class="detail-content"
      v-if="showDetail && !isNaN(answer) && !isNaN(key) && answer !== ''"
    >
      <ul>
        <li v-for="(k, index) in keyList" :key="index">
          <p class="no" :class="{ wrong: k !== answer[index] }">
            ข้อ {{ index + 1 }}
          </p>
          <p class="key">
            {{ answer[index] }}
          </p>
        </li>
      </ul>
    </div>
    <div class="result">
      <strong>
        Score: <span id="result"> {{ score }}</span>
      </strong>
      <p class="copyBtn btn" @click="copy">{{ copyText }}</p>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from "vue";

const key = ref("");
const answer = ref("");
const score = ref(0);
const copyText = ref("Click to copy");
const showDetail = ref(false);

const keyList = computed(() => {
  const list = [];
  for (const k in key.value) {
    list.push(key.value[k]);
  }

  return list;
});

const copy = () => {
  const result = score.value;
  const copyBtn = document.querySelector(".copyBtn");
  navigator.clipboard.writeText(result);

  setTimeout(() => {
    copyText.value = "Click to copy";
    copyBtn.style.color = "grey";
  }, 3000);

  copyBtn.style.color = "#4BB543";
  copyText.value = "Copied to clipboard";
};

const cal = () => {
  score.value = 0;

  for (let ans = 0; ans < answer.value.length; ans++) {
    if (key.value[ans] == answer.value[ans]) {
      score.value += 1;
    }
  }
};
</script>

<style scoped>
strong {
  font-size: 3em;
  text-align: center;
  margin-top: 0.5em;
}

ul {
  margin-top: 1em;
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  grid-gap: 0.5em 1em;
}

li {
  list-style-type: none;
  display: flex;
}

p {
  display: inline-block;
  padding: 0.5em 0.5em;
}

.form {
  display: flex;
  flex-direction: column;
}

.detail {
  text-align: center;
}

input {
  width: 80%;
  margin: 1em auto 0;
  font-size: 2em;
  padding: 0.5em 1em;
  border-radius: 1em;
  border: 1px solid black;
  text-align: center;
}

.no {
  background: lightgrey;
  text-align: right;
}

.wrong {
  background: red;
}

.key {
  text-align: center;
}

.result {
  display: flex;
  flex-direction: column;
  font-weight: bold;
}

.result p {
  text-align: center;
  font-size: 0.8em;
  width: fit-content;
  margin: auto;
}

.btn {
  cursor: pointer;
}

.copyBtn {
  color: grey;
}
</style>
