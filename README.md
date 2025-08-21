<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Show do Milhão: Olhos D’Água</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(to bottom, #ffcc00, #ff6600);
            color: #333;
            text-align: center;
            padding: 20px;
        }
        #game {
            max-width: 800px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.8);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.5);
        }
        h1 {
            color: #ff0000;
            text-shadow: 2px 2px 4px #000;
        }
        #question {
            font-size: 24px;
            margin: 20px 0;
            color: #000;
        }
        .option {
            display: block;
            width: 80%;
            margin: 10px auto;
            padding: 15px;
            background: #00ccff;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 18px;
            transition: background 0.3s;
        }
        .option:hover {
            background: #0099cc;
        }
        button {
            padding: 10px 20px;
            margin: 10px;
            background: #ff9900;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            transition: background 0.3s;
        }
        button:hover {
            background: #cc6600;
        }
        #status {
            font-size: 20px;
            margin: 20px 0;
            color: #ff0000;
        }
        #godmode-content {
            display: none;
            text-align: left;
            margin-top: 40px;
            background: #fff;
            padding: 20px;
            border-radius: 10px;
        }
        #godmode-content h2 {
            color: #ff6600;
        }
    </style>
</head>
<body>
    <div id="game">
        <h1>Show do Milhão: Olhos D’Água de Conceição Evaristo</h1>
        <div id="status">Bem-vindo! Clique em "Iniciar Jogo" para começar.</div>
        <div id="question"></div>
        <div id="options"></div>
        <button id="start">Iniciar Jogo</button>
        <button id="skip" disabled>Pular (3 restantes)</button>
        <button id="consult" disabled>Consultar Caderno (3 restantes)</button>
        <button id="quit" disabled>Desistir</button>
        <button id="godmode">God Mode</button>
        <div id="godmode-content"></div>
    </div>

    <script>
        const questions = [
            {
                q: "Qual é o título do conto?",
                options: ["Olhos de Fogo", "Olhos D’Água", "Rios de Lágrimas", "Mãe Oxum"],
                correct: 1 // B
            },
            {
                q: "Quem é a autora do conto?",
                options: ["Machado de Assis", "Conceição Evaristo", "Clarice Lispector", "Jorge Amado"],
                correct: 1 // B
            },
            {
                q: "Quantas filhas a mãe da narradora tinha?",
                options: ["5", "6", "7", "8"],
                correct: 2 // C
            },
            {
                q: "O que acordou a narradora bruscamente uma noite?",
                options: ["Um pesadelo", "Uma pergunta sobre os olhos da mãe", "Um trovão", "O choro de uma criança"],
                correct: 1 // B
            },
            {
                q: "O que a narradora não conseguia se lembrar?",
                options: ["O nome da mãe", "A cor dos olhos da mãe", "A casa da infância", "O aniversário da mãe"],
                correct: 1 // B
            },
            {
                q: "O que as filhas encontraram no cabelo da mãe, pensando ser um carrapato?",
                options: ["Um piolho", "Uma verruga", "Uma flor", "Uma bola de gude"],
                correct: 1 // B
            },
            {
                q: "Onde a mãe da narradora nasceu?",
                options: ["Rio de Janeiro", "Interior de Minas", "Bahia", "São Paulo"],
                correct: 1 // B
            },
            {
                q: "Qual brincadeira a mãe inventava para distrair a fome das filhas?",
                options: ["Esconde-esconde", "Senhora e Rainha com princesas", "Pega-pega", "Bonecas"],
                correct: 1 // B
            },
            {
                q: "O que as nuvens viravam na imaginação da narradora e da mãe?",
                options: ["Dragões", "Algodão doce", "Pássaros", "Estrelas"],
                correct: 1 // B
            },
            {
                q: "A quem a mãe rezava nos dias de fortes chuvas?",
                options: ["São Jorge", "Santa Bárbara", "Nossa Senhora", "Oxalá"],
                correct: 1 // B
            },
            {
                q: "Por que a narradora saiu de casa?",
                options: ["Para estudar", "Em busca de melhor condição de vida", "Para casar", "Para trabalhar em outra cidade"],
                correct: 1 // B
            },
            {
                q: "Quem são as Yabás mencionadas no conto?",
                options: ["Irmãs da narradora", "Ancestrais mulheres da família", "Amigas da mãe", "Vizinhos"],
                correct: 1 // B
            },
            {
                q: "O que a narradora decide fazer para lembrar a cor dos olhos da mãe?",
                options: ["Escrever uma carta", "Ligar para a mãe", "Voltar para casa", "Esquecer o assunto"],
                correct: 2 // C
            },
            {
                q: "O que a narradora viu nos olhos da mãe ao voltar?",
                options: ["Fogo", "Lágrimas", "Alegria seca", "Raiva"],
                correct: 1 // B
            },
            {
                q: "Qual é a cor dos olhos da mãe, segundo a narradora?",
                options: ["Castanho", "Azul", "Cor de olhos d’água", "Verde"],
                correct: 2 // C
            },
            {
                q: "Qual orixá é associado aos olhos da mãe?",
                options: ["Iansã", "Oxum", "Xangô", "Ogum"],
                correct: 1 // B
            },
            {
                q: "O que a filha da narradora pergunta no final?",
                options: ["Sobre a avó", "Qual é a cor tão úmida de seus olhos?", "Se pode brincar", "Sobre comida"],
                correct: 1 // B
            },
            {
                q: "Como a mãe distraía a fome das filhas?",
                options: ["Cantando", "Com brincadeiras e jogos", "Dormindo", "Lendo histórias"],
                correct: 1 // B
            },
            {
                q: "Qual era o trono da mãe na brincadeira de Rainha?",
                options: ["Uma cadeira", "Um pequeno banquinho de madeira", "A cama", "O chão"],
                correct: 1 // B
            },
            {
                q: "O que a mãe 'colhia' do céu para as filhas?",
                options: ["Estrelas", "Nuvens como algodão doce", "Pássaros", "Frutas"],
                correct: 1 // B
            }
        ];

        let shuffledQuestions = [];
        let currentQuestionIndex = 0;
        let score = 0;
        let skipsLeft = 3;
        let consultsLeft = 3;
        let gameActive = false;

        const labels = ['A', 'B', 'C', 'D'];

        function shuffle(array) {
            return array.sort(() => Math.random() - 0.5);
        }

        function startGame() {
            shuffledQuestions = shuffle([...questions]);
            currentQuestionIndex = 0;
            score = 0;
            skipsLeft = 3;
            consultsLeft = 3;
            gameActive = true;
            document.getElementById('start').style.display = 'none';
            document.getElementById('skip').disabled = false;
            document.getElementById('consult').disabled = false;
            document.getElementById('quit').disabled = false;
            updateButtons();
            showQuestion();
        }

        function showQuestion() {
            if (currentQuestionIndex >= shuffledQuestions.length) {
                endGame('Você venceu! Respondeu todas as 20 questões.');
                return;
            }
            const q = shuffledQuestions[currentQuestionIndex];
            document.getElementById('question').innerHTML = `Questão ${currentQuestionIndex + 1}/20: ${q.q}`;
            const optionsDiv = document.getElementById('options');
            optionsDiv.innerHTML = '';
            q.options.forEach((opt, i) => {
                const btn = document.createElement('button');
                btn.className = 'option';
                btn.innerHTML = `${labels[i]}) ${opt}`;
                btn.onclick = () => checkAnswer(i);
                optionsDiv.appendChild(btn);
            });
            document.getElementById('status').innerHTML = `Pontuação atual: ${score * 1000} (Prêmio fictício)`;
        }

        function checkAnswer(selected) {
            const q = shuffledQuestions[currentQuestionIndex];
            if (selected === q.correct) {
                score++;
                currentQuestionIndex++;
                showQuestion();
            } else {
                endGame('Resposta errada! Fim de jogo.');
            }
        }

        function skipQuestion() {
            if (skipsLeft > 0) {
                skipsLeft--;
                currentQuestionIndex++;
                updateButtons();
                showQuestion();
            }
        }

        function consultNotebook() {
            if (consultsLeft > 0) {
                consultsLeft--;
                const q = shuffledQuestions[currentQuestionIndex];
                let wrongIndexes = [];
                for (let i = 0; i < 4; i++) {
                    if (i !== q.correct) wrongIndexes.push(i);
                }
                wrongIndexes = shuffle(wrongIndexes).slice(0, 2);
                const optionsBtns = document.querySelectorAll('.option');
                wrongIndexes.forEach(idx => {
                    optionsBtns[idx].innerHTML += ' (Provavelmente errada - Dica do Caderno)';
                    optionsBtns[idx].disabled = true;
                });
                updateButtons();
            }
        }

        function quitGame() {
            endGame(`Você desistiu com pontuação: ${score * 1000}`);
        }

        function endGame(message) {
            gameActive = false;
            document.getElementById('status').innerHTML = message;
            document.getElementById('question').innerHTML = '';
            document.getElementById('options').innerHTML = '';
            document.getElementById('skip').disabled = true;
            document.getElementById('consult').disabled = true;
            document.getElementById('quit').disabled = true;
            document.getElementById('start').style.display = 'block';
            document.getElementById('start').innerHTML = 'Recomeçar Jogo';
        }

        function updateButtons() {
            document.getElementById('skip').innerHTML = `Pular (${skipsLeft} restantes)`;
            document.getElementById('consult').innerHTML = `Consultar Caderno (${consultsLeft} restantes)`;
        }

        function toggleGodMode() {
            const content = document.getElementById('godmode-content');
            if (content.style.display === 'block') {
                content.style.display = 'none';
            } else {
                content.innerHTML = '<h2>God Mode: Todas as Questões e Respostas</h2>';
                questions.forEach((q, idx) => {
                    const div = document.createElement('div');
                    div.innerHTML = `<p><strong>Questão ${idx + 1}:</strong> ${q.q}<br>Resposta correta: ${labels[q.correct]}) ${q.options[q.correct]}</p>`;
                    content.appendChild(div);
                });
                content.style.display = 'block';
            }
        }

        document.getElementById('start').onclick = startGame;
        document.getElementById('skip').onclick = skipQuestion;
        document.getElementById('consult').onclick = consultNotebook;
        document.getElementById('quit').onclick = quitGame;
        document.getElementById('godmode').onclick = toggleGodMode;
    </script>
</body>
</html>
