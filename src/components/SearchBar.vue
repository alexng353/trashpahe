<script setup>
import { ref, watch } from "vue";

const message = ref("");
const items = ref([]);

function OnChange() {
  fetch(`https://animepahe.com/api?m=search&q=${message.value}`)
    // fetch(`http://localhost:9999/api?m=search&q=${message.value}`)
    .then((response) => response.json())
    .then((data) => {
      console.log(data);
      items.value = data;
    });
}

watch(message, OnChange);
</script>

<style>
.searchwrapper {
  max-width: 400px;
  font-family: Inter, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    Oxygen, Ubuntu, Cantarell, "Fira Sans", "Droid Sans", "Helvetica Neue",
    sans-serif;
}

.result-wrapper {
  overflow: hidden;
  /* drop shadow 10px */
  box-shadow: 8px 8px 10px rgba(0, 0, 0, 0.2);
}

.bar {
  width: 200px;
  height: 40px;
  border-radius: 20px;
  border: 1px solid #ccc;
  text-indent: 10px;
  font-size: 16px;
  outline: none;
  transition: all 0.3s;
}

.bar:focus {
  width: 100%;
  border: 1px solid #000;
}

.poster {
  width: 100%;
  height: auto;
}

.imgwrapper {
  margin-left: 10px;
  margin-right: 10px;
  width: 50px;
  min-width: 50px;
  height: 50px;
  min-height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  border-radius: 50%;
}

.title {
  white-space: nowrap;
  width: 300px;
  overflow: hidden;
  text-overflow: ellipsis;
  /* bold */
  font-weight: bold;
}

.item {
  /* padding-top: 10px; */
  padding-top: 1px;
  padding-bottom: 1px;
  width: 400px;
  display: flex;
  align-items: center;
  height: 67px;
  background-color: #171717;
  line-height: 1;
}

.item:hover {
  background-color: #d5015b;
}

.season {
  color: #b3b3b3;
  font-size: 14px;
  margin: 0;
}

.description {
  color: #b3b3b3;
  font-size: 14px;
  margin: 2px 0;
}

a {
  text-decoration: none;
  color: white;
}

span {
  margin: 0px;
}
</style>

<template>
  <div class="searchwrapper">
    <input v-model="message" placeholder="search" class="bar" />
    <div class="result-wrapper">
      <div v-for="item in items.data" class="search-result">
        <a
          :href="'https://trash.animepahe.com/anime/' + item.session"
          class="item"
        >
          <div class="imgwrapper">
            <img :src="item.poster" class="poster" />
          </div>
          <div class="text">
            <!-- <p class="title">{{ item.title }}</p> -->
            <div class="title">{{ item.title }}</div>

            <p class="description">
              <span class="type">{{ item.type }}</span>
              <span>&nbsp;-&nbsp;</span>
              <span class="episodes">
                {{ item.episodes }} Episodes ({{ item.status }})
              </span>
            </p>
            <h1 class="season">{{ item.season }} {{ item.year }}</h1>
          </div>
        </a>
      </div>
    </div>
  </div>
</template>
