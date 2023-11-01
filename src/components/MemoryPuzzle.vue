<template>
  <div ref="phaserContainer"></div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import Phaser from 'phaser';

const theme = ref('ferme');
const phaserContainer = ref(null);
const score = ref(0)

onMounted(() => {
  const config = {
    type: Phaser.AUTO,
    width: 1500,
    height: 680,
    scene: {
      preload: preload,
      create: create,
      update: update,
    },
    physics: {
      default: 'arcade',
      arcade: {
          gravity: { y: 200 }
        }
    },
    backgroundColor: '#2c3e50', 
  };

  const game = new Phaser.Game(config);

  function preload() {
    if (theme.value === 'ferme') {
      this.load.image('rabbit', '/assets/MemoryPuzzle/theme/ferme/img_1.png');
      this.load.image('cat', '/assets/MemoryPuzzle/theme/ferme/img_2.png');
      this.load.image('goat', '/assets/MemoryPuzzle/theme/ferme/img_3.png');
      this.load.image('pig', '/assets/MemoryPuzzle/theme/ferme/img_4.png');
      this.load.image('chicken', '/assets/MemoryPuzzle/theme/ferme/img_5.png');
      this.load.image('horse', '/assets/MemoryPuzzle/theme/ferme/img_6.png');
    }
  }

  function create() {
    if (theme.value === 'ferme') {
      const listTheme = shuffleArray(['rabbit','rabbit','cat','cat','goat','goat','pig','pig','chicken','chicken','horse','horse']);
      
      const i1 = this.add.image(25, 25, listTheme[0]).setOrigin(0, 0).setScale(0.3);
      const i2 = this.add.image(250, 25, listTheme[1]).setOrigin(0, 0).setScale(0.3);
      const i3 = this.add.image(475, 25, listTheme[2]).setOrigin(0, 0).setScale(0.3);
      const i4 = this.add.image(700, 25, listTheme[3]).setOrigin(0, 0).setScale(0.3);
      const i5 = this.add.image(925, 25, listTheme[4]).setOrigin(0, 0).setScale(0.3);
      const i6 = this.add.image(1150, 25, listTheme[5]).setOrigin(0, 0).setScale(0.3);
      const i7 = this.add.image(25, 400, listTheme[6]).setOrigin(0, 0).setScale(0.3);
      const i8 = this.add.image(250, 400, listTheme[7]).setOrigin(0, 0).setScale(0.3);
      const i9 = this.add.image(475, 400, listTheme[8]).setOrigin(0, 0).setScale(0.3);
      const i10 = this.add.image(700, 400, listTheme[9]).setOrigin(0, 0).setScale(0.3);
      const i11 = this.add.image(925, 400, listTheme[10]).setOrigin(0, 0).setScale(0.3);
      const i12 = this.add.image(1150, 400, listTheme[11]).setOrigin(0, 0).setScale(0.3);
      



      // this.add.image(300, 300, 'goat').setScale(200 / 10, 200 / 10);

      const r1 = this.add.rectangle(25, 25, 200, 200, 0x9966ff).setOrigin(0, 0);
      const r2 = this.add.rectangle(250, 25, 200, 200, 0x9966ff).setOrigin(0, 0);
      const r3 = this.add.rectangle(475, 25, 200, 200, 0x9966ff).setOrigin(0, 0);
      const r4 = this.add.rectangle(700, 25, 200, 200, 0x9966ff).setOrigin(0, 0);
      const r5 = this.add.rectangle(925, 25, 200, 200, 0x9966ff).setOrigin(0, 0);
      const r6 = this.add.rectangle(1150, 25, 200, 200, 0x9966ff).setOrigin(0, 0);
      const r7 = this.add.rectangle(25, 400, 200, 200, 0x9966ff).setOrigin(0, 0);
      const r8 = this.add.rectangle(250, 400, 200, 200, 0x9966ff).setOrigin(0, 0);
      const r9 = this.add.rectangle(475, 400, 200, 200, 0x9966ff).setOrigin(0, 0);
      const r10 = this.add.rectangle(700, 400, 200, 200, 0x9966ff).setOrigin(0, 0);
      const r11 = this.add.rectangle(925, 400, 200, 200, 0x9966ff).setOrigin(0, 0);
      const r12 = this.add.rectangle(1150, 400, 200, 200, 0x9966ff).setOrigin(0, 0);

      let firstClick = true;
      let firstImg = '';
      let firstRect = '';
      const rectangles = [r1, r2, r3, r4, r5, r6, r7, r8, r9, r10, r11, r12];
      rectangles.forEach((rectangle, index) => {
      rectangle.setInteractive();
      rectangle.on('pointerdown', () => {
        if (firstClick) {
          console.log(`Nom de l'image : ${listTheme[index]}`);
          firstImg = listTheme[index];
          firstRect = rectangle;
          rectangle.setVisible(false);
          firstClick = false;
        }
        else {
          rectangle.setVisible(false);
          if (listTheme[index] === firstImg){
            score.value = score.value+1;
            firstClick = true;
          }
          else{
            setTimeout(() => {
              firstRect.setVisible(true);
              rectangle.setVisible(true);
              firstClick = true;
            }, 750);
          }
          console.log('votre score est actuellement de :',score.value)
        }
      });
    });
    }
  }

  function update() {
    // Ajoutez ici la logique de mise à jour du jeu
  }
  function shuffleArray(array) {
    for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
    }
    return array;
  }
  game.canvas.parentNode.style.width = '100%';
  game.canvas.parentNode.style.height = '100%';
  phaserContainer.value.appendChild(game.canvas);

  let isRectFlipped = false;
});
</script>

<style scoped>
  div {
    background-color: green;
    padding: 20px;
    width: 100%;
    height: 100vh;
  }
</style>
