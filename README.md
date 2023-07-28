# memorie

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
  
    <nav>
        <ul>
            <li><a href="application.html">Accueil</a></li>
            <li><a href="asitepresentation.html">Exercice</a></li>
        </ul>
    </nav>
    <div class="memory-game">
        <h1>Jeu de Memory</h1>
        <div class="cards" id="cards"></div>
        <button onclick="startGame()">Démarrer le jeu</button>
      </div>
    
 
      <script>
        let colors = ['#3498db', '#9b59b6', '#e74c3c', '#2ecc71', '#f1c40f', '#1abc9c', '#e67e22', '#95a5a6'];
        let cardsArray = [];
        let flippedCards = [];
        let gameInProgress = false;
    
        function startGame() {
          if (gameInProgress) return;
          gameInProgress = true;
    
          cardsArray = [];
          flippedCards = [];
          const cardsContainer = document.getElementById('cards');
          cardsContainer.innerHTML = '';
    
          colors = shuffleArray(colors.concat(colors));
    
          colors.forEach(color => {
            const card = createCard(color);
            cardsContainer.appendChild(card);
          });
    
          setTimeout(() => {
            flipAllCards();
            setTimeout(() => {
              flipAllCards();
              gameInProgress = false;
            }, 2000);
          }, 500);
        }
    
        function createCard(color) {
          const card = document.createElement('div');
          card.classList.add('card');
          card.dataset.color = color;
          card.addEventListener('click', flipCard);
          return card;
        }
    
        function flipAllCards() {
          const cardElements = document.querySelectorAll('.card');
          cardElements.forEach(card => {
            card.style.backgroundColor = card.classList.contains('flip') ? card.dataset.color : '';
          });
        }
    
        function shuffleArray(array) {
          for (let i = array.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [array[i], array[j]] = [array[j], array[i]];
          }
          return array;
        }
    
        function flipCard() {
          if (gameInProgress || this === flippedCards[0]) return;
    
          this.style.backgroundColor = this.dataset.color;
          this.classList.add('flip');
    
          if (flippedCards.length === 0) {
            flippedCards.push(this);
          } else if (flippedCards.length === 1) {
            flippedCards.push(this);
            checkForMatch();
          }
        }
    
        function checkForMatch() {
          const [card1, card2] = flippedCards;
          const card1Color = card1.dataset.color;
          const card2Color = card2.dataset.color;
    
          if (card1Color === card2Color) {
            matchedCards.push(card1, card2);
            flippedCards = [];
            if (matchedCards.length === colors.length) {
              setTimeout(() => {
                alert('Félicitations ! Vous avez trouvé toutes les paires !');
                startGame();
              }, 500);
            }
          } else {
            gameInProgress = true;
            setTimeout(() => {
              card1.style.backgroundColor = '';
              card2.style.backgroundColor = '';
              card1.classList.remove('flip');
              card2.classList.remove('flip');
              flippedCards = [];
              gameInProgress = false;
            }, 1000);
          }
        }
      </script>
    
</body>
</html>

<style>
 

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #292f3f;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.memory-game {
  background-color: #000000;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  max-width: 400px; 
  width: 100%; 
  text-align: center;
}

h1 {
  margin-bottom: 20px;
  color: #3498db;
}

.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(80px, 1fr)); 
  margin-bottom: 20px;
  padding: 10px;
  justify-items: center; 
}

.card {
  width: 80px;
  height: 120px; 
  background-color: #3498db;
  color: #fff;
  font-size: 24px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  border-radius: 5px;
  transition: background-color 0.3s ease;
}

.card.flip {
  background-color: #f1c40f;
}

button {
    background-color: #3498db;
  color: white;
  border: none;
  padding: 10px;
  width: 100%;
  cursor: pointer;
  border-radius: 5px;
  font-size: 16px;
  font-weight: bold;
  transition: background-color 0.3s ease;
}

button:hover {
    background-color: #287bb2;
}

/* Responsive styles */

@media screen and (max-width: 480px) {
  .cards {
    grid-template-columns: repeat(auto-fit, minmax(60px, 1fr)); 
    gap: 5px;
  }

  .card {
    width: 60px;
    height: 90px;
    font-size: 20px; 
  }
}


nav {
        background-color: #292f3f;
        padding: 10px;
        position: absolute;
        top: 10px;
        left: 10px;
        right: 10px;
        display: flex;
        justify-content: center;
        z-index: 1;
    }

    nav ul {
        list-style-type: none;
        margin: 0;
        padding: 0;
        display: flex;
        justify-content: center;
    }

    nav li {
        margin: 0 10px;
    }

    nav a {
        color: #fff;
        text-decoration: none;
        font-size: 18px;
    }

    nav a:hover {
        color: #007bff;
    }

</style>
