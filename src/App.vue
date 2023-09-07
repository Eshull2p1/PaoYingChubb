<script setup>
import { ref } from "vue";
const P1_choice = ref("");
const P2_choice = ref("");
const result = ref("");
//จำนวนคะเเนน
const score_p1 = ref(0);
const score_p2 = ref(0);

const control_game = {
  ค้อน: {
    ค้อน: "เสมอ",
    กระดาษ: "แพ้",
    กรรไกร: "ชนะ",
    เพื่อนรัก: "ชนะ",
    ความรัก: "แพ้",
  },
  กระดาษ: {
    ค้อน: "ชนะ",
    กระดาษ: "เสมอ",
    กรรไกร: "แพ้",
    เพื่อนรัก: "ชนะ",
    ความรัก: "แพ้",
  },
  กรรไกร: {
    ค้อน: "แพ้",
    กระดาษ: "ชนะ",
    กรรไกร: "เสมอ",
    เพื่อนรัก: "ชนะ",
    ความรัก: "แพ้",
  },
  เพื่อนรัก: {
    ค้อน: "แพ้",
    กระดาษ: "แพ้",
    กรรไกร: "แพ้",
    เพื่อนรัก: "เจ็บคู่",
    ความรัก: "ชนะ",
  },
  ความรัก: {
    ค้อน: "ชนะ",
    กระดาษ: "ชนะ",
    กรรไกร: "ชนะ",
    เพื่อนรัก: "แพ้",
    ความรัก: "เสมอ",
  },
};

// icone
const icone_choice = {
  ค้อน: "https://cdn.discordapp.com/attachments/989851222959874111/1149366923138695208/hammer.png",
  กระดาษ: "https://cdn.discordapp.com/attachments/989851222959874111/1149366924044677160/papper.png",
  กรรไกร: "https://cdn.discordapp.com/attachments/989851222959874111/1149366924313100401/scissors.png",
  ความรัก: "https://cdn.discordapp.com/attachments/989851222959874111/1149366923717509200/love.png",
  เพื่อนรัก: "https://cdn.discordapp.com/attachments/989851222959874111/1149366923449086013/JustFriend.png",
};

function getRandomChoice() {
  const choices = ["ค้อน", "กระดาษ", "กรรไกร", "ความรัก", "เพื่อนรัก"];
  return choices[Math.floor(Math.random() * choices.length)];
}

function Choice() {
  P1_choice.value = getRandomChoice();
  P2_choice.value = getRandomChoice();

  const out_result = control_game[P1_choice.value][P2_choice.value];

  if (out_result === "ชนะ") {
    score_p1.value++;
    result.value = "Player 1 ชนะ";
  } else if (out_result === "แพ้") {
    score_p2.value++;
    result.value = "Player 2 ชนะ";
  } else if (out_result === "เจ็บคู่") {
    score_p1.value -= 1;
    score_p2.value -= 1;
    result.value = "เจ็บคู่ -1 ทั้งสองคน";
  } else {
    result.value = "เสมอ";
  }
}

function reset_score() {
  P1_choice.value = "";
  P2_choice.value = "";
  result.value = "";
  score_p1.value = 0;
  score_p2.value = 0;
}
</script>

<template>
  <div class="contrainer">
    <h3 class="title">เกมเป่ายิงฉุบ</h3>
    <div class="contrainer_game">
      <div class="player1_display">
        <p>Player 1</p>
        <img
          v-if="P1_choice"
          :src="icone_choice[P1_choice]"
          class="img_block"
        />
        <p>{{ P1_choice }}</p>
      </div>
      <div class="player2_display">
        <p>Player 2</p>
        <img
          v-if="P2_choice"
          :src="icone_choice[P2_choice]"
          class="img_block"
        />
        <p>{{ P2_choice }}</p>
      </div>
    </div>
    <p class="winer">รอบนี้ : {{ result }}</p>
    <div class="sum_score">
      <p>คะแนน</p>
      {{ score_p1 }} ต่อ {{ score_p2 }}
    </div>
    <div class="button_block">
      <button @click="Choice" class="buttom_start">เป่ายิงฉุบ!!!</button>
      <button @click="reset_score" class="buttom_new">เริ่มใหม่</button>
    </div>
  </div>
</template>

<style>
.contrainer {
  background-color: #efa28c;
  padding-right: 20px;
  padding-left: 20px;
  border-radius: 16px;
  border: 5px solid #d08498;
  box-shadow: 2px 2px 20px 5px rgba(0, 0, 0, 0.42);
}

.img_block {
  width: 100px;
  height: 100px;
  padding: 10px;
  border: 3px solid;
  border-radius: 50px ;
  box-shadow: 0px 0px 10px 1px rgba(192, 198, 81, 0.2);
}

.contrainer_game {
  background-color: #fce8db;
  width: 500px;
  height: 250px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  align-items: stretch;
  margin: 20px;
  border-radius: 10px;
  border: 3px solid #efd582;
  box-shadow: 0px 0px 10px 8px rgba(239, 213, 130, 0.56);
}
.player1_display {
  margin-top: 5px;
  margin-bottom: 10px;
  font-weight: 700;
  color: black;
  border-right:2px solid #E0AE88;
}
.player2_display {
  margin-top: 5px;
  margin-bottom: 10px;
  font-weight: 700;
  color: black;
  border-left:2px solid #E0AE88;
}

.winer {
  background-color: #fce8db;
  margin-left: 25%;
  margin-right: 25%;
  padding: 10px;
  border-radius: 10px;
  border: 3px solid #efd582;
  box-shadow: 0px 0px 10px 8px rgba(239, 213, 130, 0.56);
  font-size: larger;
  color: black;
  font-weight: 700;
}
.sum_score {
  background-color: #fce8db;
  margin-left: 38%;
  margin-right: 38%;
  margin-bottom: 10px;
  padding-bottom: 10px;
  border-radius: 20px;
  border: 4px solid #efd582;
  box-shadow: 0px 0px 10px 8px rgba(239, 213, 130, 0.56);
  font-size: larger;
  color: black;
  font-weight: 700;
}
.buttom_start {
  margin-top: 10px;
  margin-right: 50px;
  margin-left: 25%;
  margin-bottom: 15px;
  color: black;
  font-weight: 800;
  border: 5px solid #9160b4;
  background-color: #d08498;
  box-shadow: 0px 0px 10px 8px rgba(239, 213, 130, 0.56);
}
.buttom_new {
  margin-right: 1px;
}
.title{
  font-size: x-large;
  color: black;
  text-shadow: 0px 0px 20px rgb(231, 241, 155, 3);
}
</style>
