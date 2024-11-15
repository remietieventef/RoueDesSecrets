<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>La roue des secrets - Jeu d'équipe</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            background-color: #f2f2f2;
            position: relative;
        }
        #logo {
            position: absolute;
            top: 10px;
            left: 10px;
            width: 100px;
        }
        h1 {
            font-size: 2em;
            font-weight: bold;
            background: linear-gradient(to right, red, orange, yellow, green, blue, indigo, violet);
            background-clip: text; /* Version standard */
            -webkit-background-clip: text; /* Version spécifique à WebKit */
            color: transparent;
            text-align: center;
            margin: 20px;
        }
        #wheel {
            position: relative;
            width: 300px;
            height: 300px;
            border-radius: 50%;
            border: 5px solid #333;
            overflow: hidden;
        }
        .segment {
            position: absolute;
            width: 150px;
            height: 300px;
            background-color: lightblue;
            transform-origin: 100% 50%;
            text-align: center;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            color: #333;
        }
        .segment:nth-child(1) {
            background-color: #FFDDC1;
            transform: rotate(0deg);
        }
        .segment:nth-child(2) {
            background-color: #C1FFD7;
            transform: rotate(120deg);
        }
        .segment:nth-child(3) {
            background-color: #FFD1DC;
            transform: rotate(240deg);
        }
        #spinButton, #teamSelect {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 16px;
        }
        #spinButton {
            cursor: pointer;
            background-color: #333;
            color: white;
            border: none;
            border-radius: 5px;
        }
        .team-history {
            margin-top: 20px;
            display: flex;
            gap: 20px;
            width: 100%;
            justify-content: center;
        }
        .team {
            border: 1px solid #333;
            padding: 10px;
            border-radius: 5px;
            width: 200px;
            background-color: #fff;
        }
        .team h3 {
            text-align: center;
        }
        .history {
            list-style-type: none;
            padding: 0;
        }
    </style>
</head>
<body>
    <!-- Logo EF Education First -->
    <img id="logo" src="https://www.ef.com/__/~/media/universal/efcom/logos/ef-logo-black.png" alt="EF Education First Logo">

    <!-- Titre de la board -->
    <h1>La roue des secrets</h1>

    <!-- Sélection de l'équipe -->
    <label for="teamSelect">Sélectionnez l'équipe :</label>
    <select id="teamSelect">
        <option value="teamRed">Équipe Rouge</option>
        <option value="teamGreen">Équipe Vert</option>
        <option value="teamPurple">Équipe Violet</option>
    </select>

    <div id="wheel">
        <div class="segment">Points doublés pendant 3h</div>
        <div class="segment">-10 points par équipe</div>
        <div class="segment">Points doublés pendant 3h</div>
    </div>
    <button id="spinButton">Tourner la roue</button>

    <!-- Historique des équipes -->
    <div class="team-history">
        <div class="team" id="teamRed">
            <h3>Équipe Rouge</h3>
            <ul class="history" id="historyRed"></ul>
        </div>
        <div class="team" id="teamGreen">
            <h3>Équipe Vert</h3>
            <ul class="history" id="historyGreen"></ul>
        </div>
        <div class="team" id="teamPurple">
            <h3>Équipe Violet</h3>
            <ul class="history" id="historyPurple"></ul>
        </div>
    </div>

    <script>
        const wheel = document.getElementById('wheel');
        const spinButton = document.getElementById('spinButton');
        const teamSelect = document.getElementById('teamSelect');
        const options = ["Points doublés pendant 3h", "-10 points par équipe"];
        
        const histories = {
            teamRed: document.getElementById('historyRed'),
            teamGreen: document.getElementById('historyGreen'),
            teamPurple: document.getElementById('historyPurple')
        };

        function spinWheel() {
            const randomRotation = Math.floor(Math.random() * 360) + 1440; // 1440° pour plusieurs tours
            wheel.style.transition = "transform 4s ease-out";
            wheel.style.transform = `rotate(${randomRotation}deg)`;

            setTimeout(() => {
                const selectedIndex = Math.floor((randomRotation % 360) / 120);
                const result = options[selectedIndex];
                const selectedTeam = teamSelect.value;

                // Ajouter le résultat à l'historique de l'équipe sélectionnée
                const listItem = document.createElement('li');
                listItem.textContent = result;
                histories[selectedTeam].appendChild(listItem);

                alert(`Résultat pour ${selectedTeam}: ${result}`);
            }, 4000); // Temps de rotation
        }

        spinButton.addEventListener('click', spinWheel);
    </script>
</body>
</html>
