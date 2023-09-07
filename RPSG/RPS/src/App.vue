<template>
  <div>
    <h1 class="text-center mt-5">RPS GAME!!!</h1>

    <div class="box-game d-flex justify-content-center mt-5">
      <div class="user1">
        <h3 class="text-center">DOG</h3>
        <img :src="player1ChoiceImage" alt="">
      </div>

      <div class="user2">
        <h3 class="text-center">CAT</h3>
        <img :src="player2ChoiceImage" alt="">
      </div>
    </div>

    <div class="button mt-5 d-flex justify-content-center">
      <button class="btn btn-danger" @click="playGame"  data-bs-toggle="modal" data-bs-target="#exampleModal">START</button>
      <button @click="Resetgame" class="btn btn-success mx-4">RESTART</button>
    </div>
  </div>

  <div class="score mt-3 d-flex justify-content-center">
    <div class="d-flex justify-content-center bg-success p-2 text-dark bg-opacity-25 ">

      <p class="fs-5"> SCORE {{ scorePlayer1 }} : {{ scorePlayer2 }}</p>
    </div>
</div>




    <!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h1 class="modal-title fs-5 text-center" id="exampleModalLabel">result</h1>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
      <p class="text-center fs-5 fw-bold text-danger">{{ resultMessage }}</p>
      <img :src="imagesplayer" width="250" height="250">
      </div>
     
    </div>
  </div>
</div>

</template>

<script>
export default {
  data() {
    return {
      choices: ['ค้อน', 'กระดาษ', 'กรรไกร'],
      player1Choice: '',
      player2Choice: '',
      player1ChoiceImage: 'https://media.baamboozle.com/uploads/images/52566/1589467805_71877', // รูปเริ่มต้น
      player2ChoiceImage: 'https://th.bing.com/th/id/OIP.5XMC-QRm3iDiTXSxnCn57gHaHa?pid=ImgDet&rs=1', // รูปเริ่มต้น
      resultMessage: '',
      scorePlayer1: 0, // คะแนนผู้เล่น 1
      scorePlayer2: 0,  // คะแนนผู้เล่น 2
      
    };
  },
  methods: {
    playGame() {
      const randomIndex1 = Math.floor(Math.random() * this.choices.length);
      const randomIndex2 = Math.floor(Math.random() * this.choices.length);

      this.player1Choice = this.choices[randomIndex1];
      this.player2Choice = this.choices[randomIndex2];

      this.player1ChoiceImage = this.getImagePath(this.player1Choice);
      this.player2ChoiceImage = this.getImagePath(this.player2Choice);

      this.calculateWinner();
    },
    getImagePath(choice) {
      if (choice === 'ค้อน') {
        return 'https://cdn2.vectorstock.com/i/thumb-large/63/76/raised-fist-on-white-background-colored-vector-40606376.jpg';
      } else if (choice === 'กระดาษ') {
        return 'https://i.pinimg.com/originals/2e/0e/18/2e0e18fb201e397c743d6898bb490627.jpg';
      } else if (choice === 'กรรไกร') {
        return 'https://th.bing.com/th/id/OIP.uWjt5XyC39oox2nBQuIsoQAAAA?pid=ImgDet&rs=1';
      }
    },
    calculateWinner() {
      if (this.player1Choice === this.player2Choice) {
        this.resultMessage = 'เสมอ';
        this.imagesplayer = "https://contactnumbersuk.com/wp-content/uploads/2020/12/%E0%B8%A7%E0%B8%B4%E0%B8%98%E0%B8%B5%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B8%97%E0%B8%B3%E0%B8%AB%E0%B8%A1%E0%B8%B1%E0%B8%99%E0%B8%AB%E0%B8%A1%E0%B8%B2%E0%B9%81%E0%B8%A1%E0%B8%A7.jpg"
      } else if (this.player1Choice ==="ค้อน" && this.player2Choice === "กรรไกร" || 
      this.player1Choice ==="กรรไกร" && this.player2Choice === "กระดาษ" ||
       this.player1Choice ==="กระดาษ" && this.player2Choice === "ค้อน"  ) {
        this.resultMessage = 'DOG';
        this.scorePlayer1++; // เพิ่มคะแนนผู้เล่น 1
        this.imagesplayer ='https://media.baamboozle.com/uploads/images/52566/1589467805_71877';
      } else {
        this.resultMessage = 'CAT';
        this.scorePlayer2++; // เพิ่มคะแนนผู้เล่น 2
        this.imagesplayer ='https://th.bing.com/th/id/OIP.5XMC-QRm3iDiTXSxnCn57gHaHa?pid=ImgDet&rs=1';
        
      }
    },
      Resetgame(){
        window.location.reload(); // รีเซ็ตหน้าเว็บ
      }
    
    }
  
};
</script>

<style>
.user1,.user2{
  border: 5px solid rgb(0, 0, 0);
  padding: 50px;
}
.box-game img{
  width: 200px;
  height: 200px;
}
.user1{
  margin-right: 100px;
}
.modal-body img{
margin-left: 100px;
}

</style>
