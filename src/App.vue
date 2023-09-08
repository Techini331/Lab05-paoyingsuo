
<template>
  <div class="container">
    <div class="message">เกมเป่ายิงฉุบ</div>
    <br /><br /><br />
    <br /><br /><br />
    <div class="images">
      <div class="computer">
        <div class="player-name">ฝั่งคอมพิวเตอร์</div>
        <img :src="computerChoiceImage" alt="computer" />
        <div class="computer-score">คอมพิวเตอร์: {{ computerScore }}</div> <!-- เลื่อนข้อความนับคะแนนมาที่นี่ -->
      </div>
      <div class="player">
        <div class="player-name">ฝั่งผู้เล่น</div>
        <img :src="playerChoiceImage" alt="player" />
        <div class="player-score">ผู้เล่น: {{ playerScore }}</div> <!-- เลื่อนข้อความนับคะแนนมาที่นี่ -->
      </div>
    </div>
    <div class="message">คะแนน</div>
    <br>
    <div class="points">
      คอมพิวเตอร์ <span class="computerPoints">{{ computerScore }}</span> :
      <span class="playerPoints">{{ playerScore }}</span> ผู้เล่น
    </div>
    <br /><br /><br />
    <br /><br /><br />
    <!-- เพิ่มปุ่ม "เป่ายิงฉุบ" และ "เริ่มใหม่" ที่นี่ -->
    <div class="buttons">
      <button @click="playGame">เป่ายิ๊งฉุบ</button>
      <button @click="resetGame">เริ่มใหม่</button>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      computerChoiceImage: "",
      playerChoiceImage: "",
      computerScore: 0,
      playerScore: 0,
    };
  },
  methods: {
    getRandomImage(choiceArray) {
      return choiceArray[Math.floor(Math.random() * choiceArray.length)];
    },
    
    generateRandomChoices() {
      this.computerChoiceImage = this.getRandomImage([
        "computer/stone.png",
        "computer/paper.png",
        "computer/scissor.png",
        "computer/heart.png",
      ]);
      this.playerChoiceImage = this.getRandomImage([
        "player/stone.png",
        "player/paper.png",
        "player/scissor.png",
        "player/heart.png",
      ]);
    },
    makeChoice(playerChoice) {
      const computerChoices = ['STONE', 'PAPER', 'SCISSORS'];
      const computerChoice = computerChoices[Math.floor(Math.random() * computerChoices.length)];

      // คำนวณผลและอัปเดตคะแนน
      if (playerChoice === 'STONE') {
        if (computerChoice === 'STONE') {
          // ผลเสมอ
        } else if (computerChoice === 'PAPER') {
          // คอมพิวเตอร์ชนะ
          this.computerScore++;
        } else {
          // ผู้เล่นชนะ
          this.playerScore++;
        }
      } else if (playerChoice === 'PAPER') {
        // เขียนการตัดสินใจสำหรับกรณีอื่น ๆ ให้เหมือนกัน
      } else {
        // เขียนการตัดสินใจสำหรับกรณีอื่น ๆ ให้เหมือนกัน
      }

      // สุ่มรูปภาพคอมพิวเตอร์และผู้เล่นอีกครั้ง
      this.generateRandomChoices();
    },
    playGame() {
      this.makeChoice('STONE'); // สำหรับตอนแรกคือค้อน
    },
    resetGame() {
      this.computerChoiceImage = 'computer/heart.png';
      this.playerChoiceImage = 'player/heart.png';
      this.computerScore = 0; // รีเซ็ตคะแนนคอมพิวเตอร์
      this.playerScore = 0;   // รีเซ็ตคะแนนผู้เล่น
    },
  },
  mounted() {
    this.generateRandomChoices();
  },
};
</script>