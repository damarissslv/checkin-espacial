<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>🚀 Check-in Espacial - Team Building</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --space-dark: #0a0e27;
            --space-deep: #050817;
            --neon-blue: #00d4ff;
            --neon-purple: #b829dd;
            --neon-pink: #ff2d95;
            --neon-green: #00ff88;
            --neon-yellow: #ffd700;
            --neon-orange: #ff6b35;
            --glass: rgba(255, 255, 255, 0.08);
            --glass-border: rgba(255, 255, 255, 0.15);
        }
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: 'Inter', sans-serif;
            background: var(--space-deep);
            color: #fff;
            overflow-x: hidden;
            min-height: 100vh;
        }
        #starfield {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            z-index: 0;
            pointer-events: none;
        }
        .container {
            position: relative;
            z-index: 1;
            max-width: 900px;
            margin: 0 auto;
            padding: 20px;
        }
        .header {
            text-align: center;
            padding: 40px 20px 30px;
        }
        .header h1 {
            font-family: 'Orbitron', sans-serif;
            font-size: 2rem;
            font-weight: 900;
            background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple), var(--neon-pink));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 10px;
        }
        .header p {
            color: rgba(255, 255, 255, 0.7);
            font-size: 1.1rem;
            max-width: 500px;
            margin: 0 auto;
            line-height: 1.6;
        }
        .question-box {
            background: var(--glass);
            border: 1px solid var(--glass-border);
            border-radius: 20px;
            padding: 25px;
            margin: 20px auto 30px;
            max-width: 600px;
            text-align: center;
            backdrop-filter: blur(10px);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
        }
        .question-box h2 {
            font-family: 'Orbitron', sans-serif;
            font-size: 1.3rem;
            color: var(--neon-yellow);
            margin-bottom: 8px;
        }
        .question-box p {
            color: rgba(255, 255, 255, 0.6);
            font-size: 0.95rem;
        }
        .group-section {
            margin-bottom: 25px;
            animation: fadeInUp 0.6s ease-out;
        }
        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .group-header {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 15px 20px;
            background: var(--glass);
            border: 1px solid var(--glass-border);
            border-radius: 16px;
            margin-bottom: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
            backdrop-filter: blur(10px);
        }
        .group-header:hover {
            background: rgba(255, 255, 255, 0.12);
            transform: translateX(5px);
        }
        .group-header.active {
            background: rgba(0, 212, 255, 0.15);
            border-color: var(--neon-blue);
            box-shadow: 0 0 20px rgba(0, 212, 255, 0.2);
        }
        .group-icon {
            font-size: 2rem;
            filter: drop-shadow(0 0 10px currentColor);
        }
        .group-title {
            font-family: 'Orbitron', sans-serif;
            font-size: 1.1rem;
            font-weight: 700;
            flex: 1;
        }
        .group-count {
            background: rgba(0, 0, 0, 0.4);
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 600;
            color: var(--neon-green);
            display: none;
        }
        .expand-icon {
            font-size: 1.2rem;
            transition: transform 0.3s;
            color: rgba(255, 255, 255, 0.5);
        }
        .group-header.active .expand-icon {
            transform: rotate(180deg);
        }
        .cards-container {
            display: none;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 12px;
            padding: 0 10px 15px;
        }
        .cards-container.open {
            display: grid;
        }
        .card {
            background: var(--glass);
            border: 2px solid var(--glass-border);
            border-radius: 16px;
            padding: 20px;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
            backdrop-filter: blur(10px);
        }
        .card:hover {
            transform: translateY(-3px);
            border-color: rgba(255, 255, 255, 0.3);
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.4);
        }
        .card.selected {
            border-color: var(--neon-green);
            background: rgba(0, 255, 136, 0.1);
            box-shadow: 0 0 25px rgba(0, 255, 136, 0.3), inset 0 0 20px rgba(0, 255, 136, 0.1);
        }
        .card.selected::after {
            content: '✓';
            position: absolute;
            top: 10px;
            right: 10px;
            width: 28px;
            height: 28px;
            background: var(--neon-green);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1rem;
            color: #000;
            font-weight: 700;
        }
        .card-icon {
            font-size: 2.5rem;
            margin-bottom: 10px;
            display: block;
        }
        .card-title {
            font-family: 'Orbitron', sans-serif;
            font-size: 1rem;
            font-weight: 700;
            margin-bottom: 6px;
            color: #fff;
        }
        .card-desc {
            font-size: 0.85rem;
            color: rgba(255, 255, 255, 0.7);
            line-height: 1.4;
        }
        .submit-section {
            position: sticky;
            bottom: 20px;
            text-align: center;
            padding: 20px;
            z-index: 10;
        }
        .submit-btn {
            background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple));
            border: none;
            color: white;
            padding: 18px 50px;
            font-size: 1.2rem;
            font-family: 'Orbitron', sans-serif;
            font-weight: 700;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 10px 40px rgba(0, 212, 255, 0.4);
            position: relative;
            overflow: hidden;
        }
        .submit-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 50px rgba(0, 212, 255, 0.6);
        }
        .submit-btn:disabled {
            background: #333;
            cursor: not-allowed;
            box-shadow: none;
        }
        .submit-btn .count-badge {
            position: absolute;
            top: -8px;
            right: -8px;
            background: var(--neon-pink);
            color: white;
            width: 28px;
            height: 28px;
            border-radius: 50%;
            display: none;
            align-items: center;
            justify-content: center;
            font-size: 0.85rem;
            font-weight: 700;
        }
        .results-screen {
            display: none;
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(5, 8, 23, 0.95);
            z-index: 100;
            overflow-y: auto;
            padding: 20px;
        }
        .results-screen.active {
            display: block;
        }
        .results-container {
            max-width: 800px;
            margin: 0 auto;
            padding: 40px 20px;
        }
        .results-header {
            text-align: center;
            margin-bottom: 40px;
        }
        .results-header h2 {
            font-family: 'Orbitron', sans-serif;
            font-size: 2rem;
            background: linear-gradient(135deg, var(--neon-green), var(--neon-blue));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 10px;
        }
        .total-responses {
            font-size: 1.2rem;
            color: rgba(255, 255, 255, 0.8);
            margin-bottom: 30px;
        }
        .mood-summary {
            background: var(--glass);
            border: 1px solid var(--glass-border);
            border-radius: 20px;
            padding: 25px;
            margin-bottom: 30px;
            text-align: center;
            backdrop-filter: blur(10px);
        }
        .mood-summary h3 {
            font-family: 'Orbitron', sans-serif;
            color: var(--neon-yellow);
            margin-bottom: 15px;
            font-size: 1.2rem;
        }
        .mood-text {
            font-size: 1.1rem;
            line-height: 1.6;
            color: rgba(255, 255, 255, 0.9);
        }
        .result-group {
            margin-bottom: 25px;
            background: var(--glass);
            border: 1px solid var(--glass-border);
            border-radius: 16px;
            padding: 20px;
            backdrop-filter: blur(10px);
        }
        .result-group-header {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 15px;
        }
        .result-group-header .icon {
            font-size: 1.5rem;
        }
        .result-group-header h4 {
            font-family: 'Orbitron', sans-serif;
            font-size: 1rem;
            flex: 1;
        }
        .result-group-header .percentage {
            font-size: 1.2rem;
            font-weight: 700;
            color: var(--neon-green);
        }
        .progress-bar {
            width: 100%;
            height: 8px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 4px;
            overflow: hidden;
            margin-bottom: 12px;
        }
        .progress-fill {
            height: 100%;
            border-radius: 4px;
            transition: width 1s ease-out;
        }
        .result-items {
            display: grid;
            gap: 8px;
        }
        .result-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 15px;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 10px;
            font-size: 0.9rem;
        }
        .result-item .item-count {
            font-weight: 700;
            color: var(--neon-blue);
        }
        .close-results {
            position: fixed;
            top: 20px;
            right: 20px;
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            color: white;
            width: 45px;
            height: 45px;
            border-radius: 50%;
            font-size: 1.5rem;
            cursor: pointer;
            z-index: 101;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .confirmation {
            display: none;
            position: fixed;
            top: 50%; left: 50%;
            transform: translate(-50%, -50%);
            background: var(--glass);
            border: 1px solid var(--glass-border);
            border-radius: 24px;
            padding: 40px;
            text-align: center;
            z-index: 50;
            backdrop-filter: blur(20px);
            box-shadow: 0 25px 80px rgba(0, 0, 0, 0.6);
            max-width: 90%;
            width: 400px;
        }
        .confirmation.active {
            display: block;
        }
        .confirmation-icon {
            font-size: 4rem;
            margin-bottom: 20px;
            display: block;
        }
        .confirmation h3 {
            font-family: 'Orbitron', sans-serif;
            font-size: 1.5rem;
            color: var(--neon-green);
            margin-bottom: 10px;
        }
        .confirmation p {
            color: rgba(255, 255, 255, 0.8);
            margin-bottom: 25px;
            line-height: 1.5;
        }
        .confirmation-btn {
            background: linear-gradient(135deg, var(--neon-green), var(--neon-blue));
            border: none;
            color: #000;
            padding: 14px 35px;
            font-size: 1rem;
            font-weight: 700;
            border-radius: 30px;
            cursor: pointer;
            transition: all 0.3s;
        }
        .overlay {
            display: none;
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.7);
            z-index: 40;
            backdrop-filter: blur(5px);
        }
        .overlay.active {
            display: block;
        }
        @media (max-width: 600px) {
            .header h1 { font-size: 1.5rem; }
            .cards-container { grid-template-columns: 1fr; }
            .group-header { padding: 12px 15px; }
            .card { padding: 15px; }
            .submit-btn { padding: 15px 40px; font-size: 1rem; }
        }
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: var(--space-deep); }
        ::-webkit-scrollbar-thumb { background: rgba(255, 255, 255, 0.2); border-radius: 4px; }
    </style>
</head>
<body>
    <canvas id="starfield"></canvas>
    <div class="container">
        <header class="header">
            <h1>🌌 CHECK-IN ESPACIAL</h1>
            <p>Team Building Intergaláctico<br>Descubra a energia da sua equipe hoje</p>
        </header>
        <div class="question-box">
            <h2>⚡ Qual é o seu nível de energia hoje?</h2>
            <p>Selecione uma ou mais opções que representam como você chegou para este dia</p>
        </div>
        <div id="groups-container"></div>
        <div class="submit-section">
            <button class="submit-btn" id="submitBtn" onclick="submitResponse()">
                🚀 ENVIAR RESPOSTA
                <span class="count-badge" id="countBadge">0</span>
            </button>
        </div>
    </div>
    <div class="overlay" id="overlay"></div>
    <div class="confirmation" id="confirmation">
        <span class="confirmation-icon">🎉</span>
        <h3>Check-in Enviado!</h3>
        <p>Sua energia foi registrada com sucesso!<br>Obrigado por compartilhar.</p>
        <button class="confirmation-btn" onclick="showResults()">📊 Ver Resultados da Equipe</button>
    </div>
    <div class="results-screen" id="resultsScreen">
        <button class="close-results" onclick="closeResults()">✕</button>
        <div class="results-container">
            <div class="results-header">
                <h2>📊 RESULTADOS DA EQUIPE</h2>
                <div class="total-responses" id="totalResponses">Total de respostas: 0</div>
            </div>
            <div class="mood-summary" id="moodSummary">
                <h3>🎯 Energia Geral da Equipe</h3>
                <div class="mood-text" id="moodText">Aguardando respostas...</div>
            </div>
            <div id="resultsContainer"></div>
        </div>
    </div>
    <script>
        const groupsData = [
            {
                id: 'energia', icon: '🚀', title: 'Mais Energia / Aceleração', color: '#ff6b35',
                cards: [
                    { id: 'foguete', icon: '🚀', title: 'Foguete', desc: 'Cheio de energia, querendo avançar rápido' },
                    { id: 'decolagem', icon: '🛫', title: 'Decolagem', desc: 'Começando algo importante' },
                    { id: 'propulsor', icon: '🔥', title: 'Propulsor', desc: 'Empurrando coisas para acontecer' }
                ]
            },
            {
                id: 'foco', icon: '🛰️', title: 'Foco / Observação / Estratégia', color: '#00d4ff',
                cards: [
                    { id: 'satelite', icon: '🛰️', title: 'Satélite', desc: 'Observando tudo com atenção antes de agir' },
                    { id: 'telescopio', icon: '🔭', title: 'Telescópio', desc: 'Buscando enxergar mais longe' },
                    { id: 'radar', icon: '📡', title: 'Radar', desc: 'Atento a riscos e sinais do ambiente' }
                ]
            },
            {
                id: 'estabilidade', icon: '🌟', title: 'Estabilidade / Consistência', color: '#ffd700',
                cards: [
                    { id: 'estrela', icon: '⭐', title: 'Estrela', desc: 'Constante, sustentando luz ao longo do tempo' },
                    { id: 'orbita', icon: '🔄', title: 'Órbita Estável', desc: 'Entregando com consistência e previsibilidade' },
                    { id: 'constelacao', icon: '✨', title: 'Constelação', desc: 'Conectado com outros, funcionando em rede' }
                ]
            },
            {
                id: 'intensidade', icon: '🌠', title: 'Intensidade / Momento de Pico', color: '#ff2d95',
                cards: [
                    { id: 'cometa', icon: '☄️', title: 'Cometa', desc: 'Passando com força e rapidez' },
                    { id: 'supernova', icon: '💥', title: 'Supernova', desc: 'Em um momento de grande explosão/transformação' },
                    { id: 'meteoros', icon: '🌠', title: 'Chuva de Meteoros', desc: 'Muitas coisas acontecendo ao mesmo tempo' }
                ]
            },
            {
                id: 'reflexao', icon: '🌙', title: 'Reflexão / Introspecção', color: '#b829dd',
                cards: [
                    { id: 'lua', icon: '🌙', title: 'Lua', desc: 'Mais introspectivo, refletindo e processando' },
                    { id: 'lado-oculto', icon: '🌑', title: 'Lado Oculto da Lua', desc: 'Ainda não mostrando tudo / em construção' },
                    { id: 'nebulosa', icon: '🌫️', title: 'Nebulosa', desc: 'Ideias se formando, ainda não totalmente claras' }
                ]
            },
            {
                id: 'pressao', icon: '🌍', title: 'Pressão / Desafio', color: '#ff4444',
                cards: [
                    { id: 'reentrada', icon: '🔥', title: 'Reentrada na Atmosfera', desc: 'Momento crítico, exigindo foco' },
                    { id: 'gravidade', icon: '⚖️', title: 'Gravidade Forte', desc: 'Sentindo peso/responsabilidade' },
                    { id: 'turbulencia', icon: '🌪️', title: 'Zona de Turbulência', desc: 'Lidando com incerteza' }
                ]
            },
            {
                id: 'leves', icon: '🌈', title: 'Leves / Criativos', color: '#00ff88',
                cards: [
                    { id: 'via-lactea', icon: '🌌', title: 'Via Láctea', desc: 'Cheio de possibilidades' },
                    { id: 'galaxia', icon: '🌀', title: 'Galáxia em Expansão', desc: 'Crescendo e explorando novos caminhos' },
                    { id: 'buraco', icon: '🕳️', title: 'Buraco de Minhoca', desc: 'Pensando fora da caixa / criando atalhos' }
                ]
            }
        ];
n        let selectedCards = new Set();\n        let responses = JSON.parse(localStorage.getItem('spaceCheckinResponses') || '[]');\n\n        function initStars() {\n            const canvas = document.getElementById('starfield');\n            const ctx = canvas.getContext('2d');\n            function resize() {\n                canvas.width = window.innerWidth;\n                canvas.height = window.innerHeight;\n            }\n            resize();\n            window.addEventListener('resize', resize);\n            const stars = [];\n            for (let i = 0; i < 200; i++) {\n                stars.push({\n                    x: Math.random() * canvas.width,\n                    y: Math.random() * canvas.height,\n                    size: Math.random() * 2 + 0.5,\n                    speed: Math.random() * 0.5 + 0.1,\n                    brightness: Math.random(),\n                    twinkleSpeed: Math.random() * 0.02 + 0.005\n                });\n            }\n            function animate() {\n                ctx.fillStyle = '#050817';\n                ctx.fillRect(0, 0, canvas.width, canvas.height);\n                stars.forEach(star => {\n                    star.brightness += star.twinkleSpeed;\n                    const opacity = (Math.sin(star.brightness) + 1) / 2 * 0.8 + 0.2;\n                    ctx.beginPath();\n                    ctx.arc(star.x, star.y, star.size, 0, Math.PI * 2);\n                    ctx.fillStyle = `rgba(255, 255, 255, ${opacity})`;\n                    ctx.fill();\n                    star.y += star.speed;\n                    if (star.y > canvas.height) {\n                        star.y = 0;\n                        star.x = Math.random() * canvas.width;\n                    }\n                });\n                requestAnimationFrame(animate);\n            }\n            animate();\n        }\n\n        function renderGroups() {\n            const container = document.getElementById('groups-container');\n            container.innerHTML = groupsData.map((group, index) => `\n                <div class=\"group-section\" style=\"animation-delay: ${index * 0.1}s\">\n                    <div class=\"group-header\" onclick=\"toggleGroup('${group.id}')\">\n                        <span class=\"group-icon\">${group.icon}</span>\n                        <span class=\"group-title\">${group.title}</span>\n                        <span class=\"group-count\" id=\"count-${group.id}\">0</span>\n                        <span class=\"expand-icon\">▼</span>\n                    </div>\n                    <div class=\"cards-container\" id=\"cards-${group.id}\">\n                        ${group.cards.map(card => `\n                            <div class=\"card\" id=\"card-${card.id}\" onclick=\"toggleCard('${card.id}', '${group.id}')\">\n                                <span class=\"card-icon\">${card.icon}</span>\n                                <div class=\"card-title\">${card.title}</div>\n                                <div class=\"card-desc\">${card.desc}</div>\n                            </div>\n                        `).join('')}\n                    </div>\n                </div>\n            `).join('');\n        }\n\n        function toggleGroup(groupId) {\n            const header = document.querySelector(`#cards-${groupId}`).previousElementSibling;\n            const container = document.getElementById(`cards-${groupId}`);\n            const isOpen = container.classList.contains('open');\n            document.querySelectorAll('.cards-container').forEach(c => c.classList.remove('open'));\n            document.querySelectorAll('.group-header').forEach(h => h.classList.remove('active'));\n            if (!isOpen) {\n                container.classList.add('open');\n                header.classList.add('active');\n            }\n        }\n\n        function toggleCard(cardId, groupId) {\n            event.stopPropagation();\n            const card = document.getElementById(`card-${cardId}`);\n            if (selectedCards.has(cardId)) {\n                selectedCards.delete(cardId);\n                card.classList.remove('selected');\n            } else {\n                selectedCards.add(cardId);\n                card.classList.add('selected');\n            }\n            updateCounts();\n            updateSubmitButton();\n        }\n\n        function updateCounts() {\n            groupsData.forEach(group => {\n                const count = group.cards.filter(c => selectedCards.has(c.id)).length;\n                const badge = document.getElementById(`count-${group.id}`);\n                if (badge) {\n                    badge.textContent = count;\n                    badge.style.display = count > 0 ? 'inline-block' : 'none';\n                }\n            });\n        }\n\n        function updateSubmitButton() {\n            const btn = document.getElementById('submitBtn');\n            const badge = document.getElementById('countBadge');\n            const count = selectedCards.size;\n            if (count > 0) {\n                badge.textContent = count;\n                badge.style.display = 'flex';\n                btn.disabled = false;\n            } else {\n                badge.style.display = 'none';\n                btn.disabled = true;\n            }\n        }\n\n        function submitResponse() {\n            if (selectedCards.size === 0) return;\n            const response = {\n                id: Date.now(),\n                timestamp: new Date().toISOString(),\n                cards: Array.from(selectedCards),\n                groups: groupsData.map(g => ({\n                    id: g.id,\n                    selected: g.cards.filter(c => selectedCards.has(c.id)).map(c => c.id)\n                })).filter(g => g.selected.length > 0)\n            };\n            responses.push(response);\n            localStorage.setItem('spaceCheckinResponses', JSON.stringify(responses));\n            document.getElementById('overlay').classList.add('active');\n            document.getElementById('confirmation').classList.add('active');\n            selectedCards.clear();\n            document.querySelectorAll('.card').forEach(c => c.classList.remove('selected'));\n            updateCounts();\n            updateSubmitButton();\n        }\n\n        function showResults() {\n            document.getElementById('overlay').classList.remove('active');\n            document.getElementById('confirmation').classList.remove('active');\n            document.getElementById('resultsScreen').classList.add('active');\n            renderResults();\n        }\n\n        function renderResults() {\n            const total = responses.length;\n            document.getElementById('totalResponses').textContent = `Total de respostas: ${total}`;\n            if (total === 0) {\n                document.getElementById('moodText').textContent = 'Aguardando respostas...';\n                document.getElementById('resultsContainer').innerHTML = '';\n                return;\n            }\n            const stats = {};\n            groupsData.forEach(g => {\n                stats[g.id] = { group: g, total: 0, cards: {} };\n                g.cards.forEach(c => { stats[g.id].cards[c.id] = 0; });\n            });\n            responses.forEach(r => {\n                r.cards.forEach(cardId => {\n                    groupsData.forEach(g => {\n                        const card = g.cards.find(c => c.id === cardId);\n                        if (card) {\n                            stats[g.id].total++;\n                            stats[g.id].cards[cardId]++;\n                        }\n                    });\n                });\n            });\n            let maxGroup = null;\n            let maxCount = 0;\n            Object.values(stats).forEach(s => {\n                if (s.total > maxCount) {\n                    maxCount = s.total;\n                    maxGroup = s.group;\n                }\n            });\n            if (maxGroup) {\n                document.getElementById('moodText').innerHTML = \n                    `A energia predominante da equipe é <strong style=\"color: ${maxGroup.color}\">${maxGroup.title}</strong> ` +\n                    `com <strong>${maxCount}</strong> seleções! 🚀`;\n            }\n            const resultsHtml = Object.values(stats)\n                .filter(s => s.total > 0)\n                .sort((a, b) => b.total - a.total)\n                .map(s => {\n                    const percentage = Math.round((s.total / (total * 3)) * 100);\n                    const cardsHtml = Object.entries(s.cards)\n                        .filter(([_, count]) => count > 0)\n                        .sort(([_, a], [__, b]) => b - a)\n                        .map(([cardId, count]) => {\n                            const card = s.group.cards.find(c => c.id === cardId);\n                            return `\n                                <div class=\"result-item\">\n                                    <span class=\"item-name\">${card.icon} ${card.title}</span>\n                                    <span class=\"item-count\">${count} pessoa${count !== 1 ? 's' : ''}</span>\n                                </div>\n                            `;\n                        }).join('');\n                    return `\n                        <div class=\"result-group\">\n                            <div class=\"result-group-header\">\n                                <span class=\"icon\">${s.group.icon}</span>\n                                <h4>${s.group.title}</h4>\n                                <span class=\"percentage\">${s.total} votos</span>\n                            </div>\n                            <div class=\"progress-bar\">\n                                <div class=\"progress-fill\" style=\"width: ${Math.min(percentage * 3, 100)}%; background: ${s.group.color}\"></div>\n                            </div>\n                            <div class=\"result-items\">\n                                ${cardsHtml}\n                            </div>\n                        </div>\n                    `;\n                }).join('');\n            document.getElementById('resultsContainer').innerHTML = resultsHtml;\n        }\n\n        function closeResults() {\n            document.getElementById('resultsScreen').classList.remove('active');\n        }\n\n        window.onload = function() {\n            initStars();\n            renderGroups();\n            updateSubmitButton();\n        };\n    </script>\n</body>\n</html>
