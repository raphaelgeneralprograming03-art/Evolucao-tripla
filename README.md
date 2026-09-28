
<html lang="pt-BR" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simulador da Escala de Kardashev: Da Transição ao Domínio Galáctico</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons CDN -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <!-- Chart.js CDN -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        kardashev: {
                            base: '#030712',
                            card: '#0f172a',
                            border: '#1e293b',
                            accent: '#38bdf8'
                        }
                    },
                    animation: {
                        'pulse-glow': 'pulseGlow 2.5s infinite alternate',
                        'flow-fast': 'flowAnimation 1s linear infinite',
                        'flow-slow': 'flowAnimation 4s linear infinite',
                    },
                    keyframes: {
                        pulseGlow: {
                            '0%': { boxShadow: '0 0 10px rgba(56, 189, 248, 0.2)' },
                            '100%': { boxShadow: '0 0 30px rgba(168, 85, 247, 0.6)' }
                        },
                        flowAnimation: {
                            '0%': { backgroundPosition: '0% 50%' },
                            '100%': { backgroundPosition: '100% 50%' }
                        }
                    }
                }
            }
        }
    </script>

    <style>
        body {
            background-color: #030712;
            color: #f8fafc;
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            overflow-x: hidden;
        }

        .glass-panel {
            background: rgba(15, 23, 42, 0.75);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(56, 189, 248, 0.15);
        }

        .glass-panel-active {
            border-color: rgba(56, 189, 248, 0.5);
            box-shadow: 0 0 25px rgba(56, 189, 248, 0.15);
        }

        /* Animação de Canvas */
        #viewportCanvas {
            background: radial-gradient(circle at center, #0B0F19 0%, #030712 100%);
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #030712;
        }
        ::-webkit-scrollbar-thumb {
            background: #1e293b;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #38bdf8;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between antialiased selection:bg-cyan-500 selection:text-black">

    <!-- HEADER DE NAVEGAÇÃO -->
    <header class="glass-panel sticky top-0 z-50 border-b border-slate-800 px-4 lg:px-8 py-3">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4">
            <div class="flex items-center space-x-3">
                <div class="p-2.5 bg-gradient-to-tr from-cyan-600 to-purple-600 rounded-xl text-white shadow-lg shadow-cyan-950">
                    <i data-lucide="layers" class="w-6 h-6"></i>
                </div>
                <div>
                    <h1 class="text-lg md:text-xl font-extrabold bg-clip-text text-transparent bg-gradient-to-r from-cyan-400 via-purple-300 to-pink-400">
                        SIMULADOR INTEGRADO DA ESCALA DE KARDASHEV
                    </h1>
                    <p class="text-xs text-slate-400 flex items-center gap-1">
                        <span>Acompanhamento Evolutivo da Civilização Humana</span>
                    </p>
                </div>
            </div>

            <!-- SELETOR DE NÍVEIS -->
            <div class="flex items-center bg-slate-900/90 p-1.5 rounded-xl border border-slate-800 gap-1 overflow-x-auto max-w-full">
                <button onclick="setLevel('0.732')" id="btn-0.732" class="level-btn px-3 py-1.5 rounded-lg text-xs font-semibold transition-all flex items-center gap-1.5 whitespace-nowrap bg-cyan-500/20 text-cyan-300 border border-cyan-500/40">
                    <i data-lucide="flame" class="w-3.5 h-3.5"></i> K-0.732 (Atual)
                </button>
                <button onclick="setLevel('1.000')" id="btn-1.000" class="level-btn px-3 py-1.5 rounded-lg text-xs font-semibold transition-all flex items-center gap-1.5 whitespace-nowrap text-slate-400 hover:text-white">
                    <i data-lucide="globe" class="w-3.5 h-3.5"></i> K-1.000 (Planetária)
                </button>
                <button onclick="setLevel('2.000')" id="btn-2.000" class="level-btn px-3 py-1.5 rounded-lg text-xs font-semibold transition-all flex items-center gap-1.5 whitespace-nowrap text-slate-400 hover:text-white">
                    <i data-lucide="sun" class="w-3.5 h-3.5"></i> K-2.000 (Estelar)
                </button>
                <button onclick="setLevel('3.000')" id="btn-3.000" class="level-btn px-3 py-1.5 rounded-lg text-xs font-semibold transition-all flex items-center gap-1.5 whitespace-nowrap text-slate-400 hover:text-white">
                    <i data-lucide="orbit" class="w-3.5 h-3.5"></i> K-3.000 (Galáctica)
                </button>
            </div>
        </div>
    </header>

    <!-- VISÃO GERAL DO APLICATIVO & CONTEXTO HISTÓRICO/EVOLUTIVO -->
    <section class="max-w-7xl mx-auto w-full px-4 lg:px-8 mt-6">
        <div class="glass-panel p-5 rounded-2xl border border-cyan-500/20 relative overflow-hidden">
            <div class="flex flex-col lg:flex-row items-start lg:items-center justify-between gap-6">
                <div class="space-y-2 max-w-3xl">
                    <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-cyan-950/80 border border-cyan-500/30 text-cyan-300 text-xs font-medium">
                        <i data-lucide="sparkles" class="w-3.5 h-3.5 text-cyan-400"></i>
                        Visão Geral do Aplicativo
                    </div>
                    <h2 id="levelTitle" class="text-xl md:text-2xl font-bold text-white">Nível 0.732: A Transição Crítica (Civilização Fóssil)</h2>
                    <p id="levelDesc" class="text-xs md:text-sm text-slate-300 leading-relaxed">
                        Atualmente extraímos energia de combustíveis fósseis e renováveis incipientes. Estamos vulneráveis ao Grande Filtro, enfrentando colapso climático e instabilidade geopolítica enquanto tentamos dominar a fusão nuclear comercial e a captura de carbono.
                    </p>
                </div>

                <!-- CARDS DE MÉTRICAS EM TEMPO REAL -->
                <div class="grid grid-cols-2 md:grid-cols-3 gap-3 w-full lg:w-auto">
                    <div class="bg-slate-900/80 p-3 rounded-xl border border-slate-800">
                        <div class="text-[11px] text-slate-400 flex items-center gap-1">
                            <i data-lucide="zap" class="w-3 h-3 text-yellow-400"></i> Potência Total
                        </div>
                        <div id="statPower" class="text-sm md:text-base font-mono font-bold text-cyan-300 mt-1">1.8 × 10¹³ W</div>
                    </div>

                    <div class="bg-slate-900/80 p-3 rounded-xl border border-slate-800">
                        <div class="text-[11px] text-slate-400 flex items-center gap-1">
                            <i data-lucide="users" class="w-3 h-3 text-purple-400"></i> População
                        </div>
                        <div id="statPop" class="text-sm md:text-base font-mono font-bold text-purple-300 mt-1">8.1 Bilhões</div>
                    </div>

                    <div class="bg-slate-900/80 p-3 rounded-xl border border-slate-800 col-span-2 md:col-span-1">
                        <div class="text-[11px] text-slate-400 flex items-center gap-1">
                            <i data-lucide="shield-alert" class="w-3 h-3 text-red-400"></i> Risco do Grande Filtro
                        </div>
                        <div id="statFilter" class="text-sm md:text-base font-mono font-bold text-red-400 mt-1">Altíssimo (68%)</div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- CONTEÚDO PRINCIPAL: SIMULAÇÃO GRÁFICA + TECNOLOGIAS POR DOMÍNIO/ZONA -->
    <main class="max-w-7xl mx-auto w-full px-4 lg:px-8 py-6 space-y-6">

        <!-- SIMULADOR GRÁFICO 2D/CANVAS DE MOBILIDADE E AMBIENTES -->
        <div class="glass-panel p-4 rounded-2xl border border-slate-800 space-y-3">
            <div class="flex flex-col md:flex-row md:items-center justify-between gap-2">
                <div class="flex items-center gap-2">
                    <i data-lucide="eye" class="w-5 h-5 text-cyan-400"></i>
                    <h3 class="text-sm font-bold text-white">Simulação Visual do Cenário & Tráfego de Veículos</h3>
                </div>
                <div class="flex items-center gap-3 text-xs text-slate-400">
                    <span class="flex items-center gap-1"><span class="w-2.5 h-2.5 rounded-full bg-cyan-400"></span> Veículos Urbanos/Rurais</span>
                    <span class="flex items-center gap-1"><span class="w-2.5 h-2.5 rounded-full bg-yellow-400"></span> Logística Mar/Ar</span>
                    <span class="flex items-center gap-1"><span class="w-2.5 h-2.5 rounded-full bg-purple-400"></span> Tráfego Espacial</span>
                </div>
            </div>

            <!-- CANVAS DINÂMICO -->
            <div class="relative w-full h-72 rounded-xl overflow-hidden border border-slate-800 shadow-inner">
                <canvas id="viewportCanvas" class="w-full h-full block"></canvas>
                <div class="absolute bottom-3 left-3 bg-slate-950/80 backdrop-blur px-3 py-1.5 rounded-lg border border-slate-800 text-[11px] font-mono text-cyan-300" id="canvasStatus">
                    Ambiente Ativo: Terra / Mar / Ar / Espaço em Kardashev 0.732
                </div>
            </div>
        </div>

        <!-- TABELA/SEÇÃO DE TECNOLOGIAS POR DOMÍNIO E ZONA -->
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">

            <!-- COLUNA 1: AMBIENTES FÍSICOS (MAR, TERRA, AR, ESPAÇO) -->
            <div class="glass-panel p-5 rounded-2xl border border-slate-800 space-y-4">
                <div class="flex items-center justify-between border-b border-slate-800 pb-3">
                    <h3 class="text-base font-bold text-white flex items-center gap-2">
                        <i data-lucide="compass" class="w-5 h-5 text-cyan-400"></i>
                        Tecnologias por Ambientes
                    </h3>
                    <span class="text-xs text-slate-400">Infraestrutura Física</span>
                </div>

                <div class="space-y-3">
                    <!-- MAR -->
                    <div class="p-3 bg-slate-900/60 rounded-xl border border-slate-800/80 hover:border-cyan-500/30 transition-all">
                        <div class="flex items-center gap-2 text-xs font-bold text-cyan-300 mb-1">
                            <i data-lucide="waves" class="w-4 h-4"></i> No Mar
                        </div>
                        <p id="techSea" class="text-xs text-slate-300 leading-relaxed">
                            Dessalinização por osmose reversa pesada; início da mineração submarina robotizada; fazendas artificiais de algas em estágio inicial.
                        </p>
                    </div>

                    <!-- TERRA -->
                    <div class="p-3 bg-slate-900/60 rounded-xl border border-slate-800/80 hover:border-cyan-500/30 transition-all">
                        <div class="flex items-center gap-2 text-xs font-bold text-emerald-300 mb-1">
                            <i data-lucide="mountain" class="w-4 h-4"></i> Na Terra
                        </div>
                        <p id="techLand" class="text-xs text-slate-300 leading-relaxed">
                            Usinas térmicas a carvão/gás coexistindo com parques eólicos e solares; agricultura intensiva com pesticidas; desmatamento ainda ativo.
                        </p>
                    </div>

                    <!-- AR -->
                    <div class="p-3 bg-slate-900/60 rounded-xl border border-slate-800/80 hover:border-cyan-500/30 transition-all">
                        <div class="flex items-center gap-2 text-xs font-bold text-sky-300 mb-1">
                            <i data-lucide="wind" class="w-4 h-4"></i> No Ar
                        </div>
                        <p id="techAir" class="text-xs text-slate-300 leading-relaxed">
                            Aviação comercial movida a querosene de aviação (jet fuel); protótipos de captura direta de carbono (DAC) de baixa escala.
                        </p>
                    </div>

                    <!-- ESPAÇO -->
                    <div class="p-3 bg-slate-900/60 rounded-xl border border-slate-800/80 hover:border-cyan-500/30 transition-all">
                        <div class="flex items-center gap-2 text-xs font-bold text-purple-300 mb-1">
                            <i data-lucide="rocket" class="w-4 h-4"></i> No Espaço
                        </div>
                        <p id="techSpace" class="text-xs text-slate-300 leading-relaxed">
                            Foguetes químicos reutilizáveis; Estação Espacial Internacional e postos orbitais privados; robôs exploradores em Marte e na Lua.
                        </p>
                    </div>
                </div>
            </div>

            <!-- COLUNA 2: ZONAS POPULACIONAIS & MOBILIDADE DOS VEÍCULOS -->
            <div class="glass-panel p-5 rounded-2xl border border-slate-800 space-y-4">
                <div class="flex items-center justify-between border-b border-slate-800 pb-3">
                    <h3 class="text-base font-bold text-white flex items-center gap-2">
                        <i data-lucide="map-pin" class="w-5 h-5 text-purple-400"></i>
                        Tecnologias por Zonas & Mobilidade
                    </h3>
                    <span class="text-xs text-slate-400">Habitação & Veículos</span>
                </div>

                <div class="space-y-3">
                    <!-- ZONA URBANA -->
                    <div class="p-3 bg-slate-900/60 rounded-xl border border-slate-800/80 hover:border-purple-500/30 transition-all">
                        <div class="flex items-center gap-2 text-xs font-bold text-purple-300 mb-1">
                            <i data-lucide="building-2" class="w-4 h-4"></i> Zona Urbana
                        </div>
                        <p id="zoneUrban" class="text-xs text-slate-300 leading-relaxed">
                            Metrópoles horizontais expansivas com ilhas de calor; transição lenta de veículos a combustão para elétricos (EVs); congestionamentos crônicos.
                        </p>
                    </div>

                    <!-- ZONA RURAL -->
                    <div class="p-3 bg-slate-900/60 rounded-xl border border-slate-800/80 hover:border-purple-500/30 transition-all">
                        <div class="flex items-center gap-2 text-xs font-bold text-yellow-300 mb-1">
                            <i data-lucide="tractor" class="w-4 h-4"></i> Zona Rural
                        </div>
                        <p id="zoneRural" class="text-xs text-slate-300 leading-relaxed">
                            Monoculturas extensivas; tratores diesel semi-autônomos via GPS; dependência de fertilizantes sintéticos derivados do petróleo.
                        </p>
                    </div>

                    <!-- ZONA DESÉRTICA -->
                    <div class="p-3 bg-slate-900/60 rounded-xl border border-slate-800/80 hover:border-purple-500/30 transition-all">
                        <div class="flex items-center gap-2 text-xs font-bold text-orange-300 mb-1">
                            <i data-lucide="sun-medium" class="w-4 h-4"></i> Zona Desértica
                        </div>
                        <p id="zoneDesert" class="text-xs text-slate-300 leading-relaxed">
                            Regiões inóspitas com vastas usinas solares fotovoltaicas de baixa eficiência; estradas isoladas para transporte rodoviário pesado.
                        </p>
                    </div>

                    <!-- DINÂMICA DE VEÍCULOS & POPULAÇÃO -->
                    <div class="p-3 bg-slate-900/60 rounded-xl border border-slate-800/80 hover:border-purple-500/30 transition-all">
                        <div class="flex items-center gap-2 text-xs font-bold text-pink-300 mb-1">
                            <i data-lucide="car" class="w-4 h-4"></i> Movimentação da População & Veículos
                        </div>
                        <p id="vehicPop" class="text-xs text-slate-300 leading-relaxed">
                            Carros individuais a gasolina/bateria, trens de alta velocidade locais, navios cargueiros a óleo pesado e aviões a jato cruzando a atmosfera baixa.
                        </p>
                    </div>
                </div>
            </div>

        </div>

        <!-- GRÁFICO HISTÓRICO COMPARATIVO DA ESCALA KARDASHEV -->
        <div class="glass-panel p-5 rounded-2xl border border-slate-800 space-y-3">
            <div class="flex items-center justify-between border-b border-slate-800 pb-3">
                <h3 class="text-base font-bold text-white flex items-center gap-2">
                    <i data-lucide="line-chart" class="w-5 h-5 text-cyan-400"></i>
                    Comparativo Exponencial do Consumo Energético (Watts)
                </h3>
                <span class="text-xs font-mono text-slate-400">Escala de 10¹³ W até 10³⁷ W</span>
            </div>
            <div class="relative w-full h-56">
                <canvas id="kardashevComparisonChart"></canvas>
            </div>
        </div>

    </main>

    <!-- FOOTER -->
    <footer class="glass-panel border-t border-slate-800 py-4 px-4 text-center text-xs text-slate-400 mt-auto">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-2">
            <div>Simulador Evolutivo Kardashev • Da Civilização 0.732 à 3.000</div>
            <div class="text-slate-500">Desenvolvido para análise de cenários tecnológicos e energéticos futuros</div>
        </div>
    </footer>

    <!-- SCRIPT DE LÓGICA E DADOS DOS NÍVEIS -->
    <script>
        // DADOS DETALHADOS DE CADA NÍVEL DA ESCALA
        const kardashevData = {
            "0.732": {
                title: "Nível 0.732: A Transição Crítica (Civilização Fóssil)",
                desc: "Atualmente extraímos energia de combustíveis fósseis e renováveis incipientes. Estamos vulneráveis ao Grande Filtro, enfrentando colapso climático e instabilidade geopolítica enquanto tentamos dominar a fusão nuclear comercial e a captura de carbono.",
                power: "1.8 × 10¹³ W",
                pop: "8.1 Bilhões",
                filter: "Altíssimo (68%)",
                techSea: "Dessalinização por osmose reversa pesada; início da mineração submarina robotizada; fazendas artificiais de algas em estágio inicial.",
                techLand: "Usinas térmicas a carvão/gás coexistindo com parques eólicos e solares; agricultura intensiva com pesticidas; desmatamento ainda ativo.",
                techAir: "Aviação comercial movida a querosene de aviação (jet fuel); protótipos de captura direta de carbono (DAC) de baixa escala.",
                techSpace: "Foguetes químicos reutilizáveis; Estação Espacial Internacional e postos orbitais privados; robôs exploradores em Marte e na Lua.",
                zoneUrban: "Metrópoles horizontais expansivas com ilhas de calor; transição lenta de veículos a combustão para elétricos (EVs); congestionamentos crônicos.",
                zoneRural: "Monoculturas extensivas; tratores diesel semi-autônomos via GPS; dependência de fertilizantes sintéticos derivados do petróleo.",
                zoneDesert: "Regiões inóspitas com vastas usinas solares fotovoltaicas de baixa eficiência; estradas isoladas para transporte rodoviário pesado.",
                vehicPop: "Carros individuais a gasolina/bateria, trens de alta velocidade locais, navios cargueiros a óleo pesado e aviões a jato cruzando a atmosfera baixa.",
                canvasLabel: "Tráfego K-0.73: Rodovias terrestres, frota naval e aeronaves a jato",
                particleType: "fossil"
            },
            "1.000": {
                title: "Nível 1.000: Civilização Planetária Integra (Controle da Terra)",
                desc: "A humanidade captura e controla toda a energia incidente na Terra (~10¹⁶ W). O clima é geoengenheirado, a fusão nuclear é abundante, a AGI gerencia a infraestrutura e o espaço próximo é dominado por elevadores espaciais de nanotubos.",
                power: "1.0 × 10¹⁶ W",
                pop: "12.0 Bilhões",
                filter: "Superado (2%)",
                techSea: "Dessalinização massiva impulsionada por fusão; cidades flutuantes autossuficientes; mineração submarina 100% robótica e sustentável.",
                techLand: "Substituição total de térmicas por reatores de fusão e redes solares globais; cidades verticais megasustentáveis e reflorestamento total.",
                techAir: "Captura massiva de CO₂ atmosférico revertendo o aquecimento global; frotas aéreas comerciais 100% elétricas ou a hidrogênio magnético.",
                techSpace: "Elevadores espaciais de nanotubos de carbono; limpeza total do lixo orbital; indústrias de manufatura em gravidade zero e bases lunares.",
                zoneUrban: "Arcologias verticais com microclima controlado, transporte público maglev subterrâneo e zero poluição sonora ou atmosférica.",
                zoneRural: "Fazendas verticais automatizadas em torres urbanas; recuperação de florestas nativas nas antigas áreas rurais industriais.",
                zoneDesert: "Desertos transformados em oásis produtivos via irrigação por fusão e espelhos refletores orbitais ajustáveis.",
                vehicPop: "Pods autônomos levitantes (Maglev), eVTOLs atmosféricos, trens hiperloop tubulares e elevadores espaciais contínuos.",
                canvasLabel: "Tráfego K-1.0: Pods Maglev, VTOLs elétricos e Elevadores Espaciais",
                particleType: "planetary"
            },
            "2.000": {
                title: "Nível 2.000: Civilização Estelar (O Domínio do Sistema Solar)",
                desc: "A humanidade constrói um Enxame de Dyson ao redor do Sol, capturando ~10²⁶ W. Mercúrio é desmantelado por sondas autorreplicantes de Von Neumann. Marte e Vênus são terraformados e a população vive em habitats tipo Cilindros de O'Neill.",
                power: "3.8 × 10²⁶ W",
                pop: "2.5 Trilhões",
                filter: "Inexistente (0%)",
                techSea: "Oceanos artificiais criados em Marte e restauração completa dos oceanos terrestres como reservas biológicas virgens.",
                techLand: "A Terra é um parque histórico preservado livre de indústrias pesadas; mineração transferida integralmente para os asteroides e Mercúrio.",
                techAir: "Atmosferas artificiais densas criadas em Marte e Vênus com controle de densidade e composição via bio-engenharia.",
                techSpace: "Enxame de Dyson com bilhões de coletores orbitais; Star Lifting (mineração do Sol); frotas com motores de antimatéria e velas de fótons.",
                zoneUrban: "Cilindros de O'Neill em órbita simulando gravidade por rotação; megacidades orbitais sustentando centenas de milhões de mentes cada.",
                zoneRural: "Mundos agrícolas estufas em habitats espaciais controlando fotoperíodo e gravidade para rendimento alimentar máximo.",
                zoneDesert: "Superfícies planetárias inóspitas cobertas por computadores de Matrioshka Brain e refinarias de fusão de Hélio-3.",
                vehicPop: "Naves com propulsão por antimatéria, velas solares impulsionadas por laser e shuttles espaciais entre mundos terraformados.",
                canvasLabel: "Tráfego K-2.0: Frotas de Antimatéria e Tráfego do Enxame de Dyson",
                particleType: "stellar"
            },
            "3.000": {
                title: "Nível 3.000: Civilização Galáctica (O Domínio da Via Láctea)",
                desc: "Comanda a energia de 200 bilhões de estrelas (~10³⁷ W) e do buraco negro Sagittarius A* via Processo Penrose. A humanidade é pós-biológica, digital, imortal e interconectada por buracos de minhoca e motores de dobra espacial.",
                power: "1.0 × 10³⁷ W",
                pop: "10²⁰ Mentes Digitais",
                filter: "Inexistente (0%)",
                techSea: "Mundos oceânicos inteiramente construídos de forma artificial para simulações biológicas exóticas e preservação biológica.",
                techLand: "Planetas inteiros convertidos em supercomputadores (Matrioshka Brains) e nós estruturais da rede galáctica.",
                techAir: "Atmosferas manipuladas por campos de força gravitacionais; voos sem atrito através de manipulação direta do espaço-tempo.",
                techSpace: "Enxames de Dyson em todas as estrelas úteis; usinas na ergosfera de buracos negros; motores de dobra Alcubierre e redes FTL.",
                zoneUrban: "Capitais computacionais em redor de Sagittarius A*; esferas de dados com mentes virtuais simulando universos inteiros.",
                zoneRural: "Sistemas estelares reorganizados por Propulsores Shkadov para evitar supernovas e otimizar a distribuição de massa.",
                zoneDesert: "Espaço profundo interstelático preenchido por colhedores de Matéria Escura e ancoragens gravitacionais artificiais.",
                vehicPop: "Naves de Dobra Espacial (Alcubierre), transmissão instantânea de mentes via rede quantica e portais de buracos de minhoca.",
                canvasLabel: "Tráfego K-3.0: Dobra Espacial (FTL), Buracos de Minhoca e Mentes Virtuais",
                particleType: "galactic"
            }
        };

        let currentLevel = "0.732";
        let chartInstance = null;

        // INICIALIZAÇÃO
        document.addEventListener('DOMContentLoaded', () => {
            lucide.createIcons();
            initChart();
            initCanvas();
            setLevel('0.732');
        });

        // MUDANÇA DE NÍVEL
        function setLevel(lvl) {
            currentLevel = lvl;
            const data = kardashevData[lvl];

            // Atualizar botões
            document.querySelectorAll('.level-btn').forEach(btn => {
                btn.className = "level-btn px-3 py-1.5 rounded-lg text-xs font-semibold transition-all flex items-center gap-1.5 whitespace-nowrap text-slate-400 hover:text-white";
            });
            const activeBtn = document.getElementById(`btn-${lvl}`);
            activeBtn.className = "level-btn px-3 py-1.5 rounded-lg text-xs font-semibold transition-all flex items-center gap-1.5 whitespace-nowrap bg-cyan-500/20 text-cyan-300 border border-cyan-500/40";

            // Atualizar textos e métricas
            document.getElementById('levelTitle').innerText = data.title;
            document.getElementById('levelDesc').innerText = data.desc;
            document.getElementById('statPower').innerText = data.power;
            document.getElementById('statPop').innerText = data.pop;
            document.getElementById('statFilter').innerText = data.filter;

            // Atualizar Domínios
            document.getElementById('techSea').innerText = data.techSea;
            document.getElementById('techLand').innerText = data.techLand;
            document.getElementById('techAir').innerText = data.techAir;
            document.getElementById('techSpace').innerText = data.techSpace;

            // Atualizar Zonas
            document.getElementById('zoneUrban').innerText = data.zoneUrban;
            document.getElementById('zoneRural').innerText = data.zoneRural;
            document.getElementById('zoneDesert').innerText = data.zoneDesert;
            document.getElementById('vehicPop').innerText = data.vehicPop;

            // Canvas Label
            document.getElementById('canvasStatus').innerText = data.canvasLabel;

            // Resetar simulação visual
            resetVehicleParticles();
        }

        // GRÁFICO CHART.JS COMPARATIVO
        function initChart() {
            const ctx = document.getElementById('kardashevComparisonChart').getContext('2d');
            chartInstance = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['K-0.732 (Atual)', 'K-1.000 (Planetária)', 'K-2.000 (Estelar)', 'K-3.000 (Galáctica)'],
                    datasets: [{
                        label: 'Potência Energética Estimada (Expoente Log10 em Watts)',
                        data: [13.25, 16.00, 26.58, 37.00],
                        backgroundColor: [
                            'rgba(6, 182, 212, 0.7)',
                            'rgba(16, 185, 129, 0.7)',
                            'rgba(245, 158, 11, 0.7)',
                            'rgba(168, 85, 247, 0.7)'
                        ],
                        borderColor: [
                            '#06b6d4',
                            '#10b981',
                            '#f59e0b',
                            '#a855f7'
                        ],
                        borderWidth: 1.5,
                        borderRadius: 8
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            title: { display: true, text: 'Potência em Watts (10^x W)', color: '#94a3b8' },
                            grid: { color: 'rgba(30, 41, 59, 0.5)' },
                            ticks: { color: '#94a3b8' },
                            min: 10,
                            max: 40
                        },
                        x: {
                            grid: { display: false },
                            ticks: { color: '#f8fafc', font: { size: 11 } }
                        }
                    },
                    plugins: {
                        legend: { labels: { color: '#f8fafc' } }
                    }
                }
            });
        }

        // SIMULAÇÃO VISUAL EM CANVAS (VEÍCULOS E TRÁFEGO)
        let particles = [];
        let canvas, ctx;

        function initCanvas() {
            canvas = document.getElementById('viewportCanvas');
            ctx = canvas.getContext('2d');

            function resize() {
                canvas.width = canvas.parentElement.clientWidth;
                canvas.height = canvas.parentElement.clientHeight;
            }
            resize();
            window.addEventListener('resize', resize);

            resetVehicleParticles();
            requestAnimationFrame(animateCanvas);
        }

        function resetVehicleParticles() {
            particles = [];
            const count = 40;
            for (let i = 0; i < count; i++) {
                particles.push({
                    x: Math.random() * canvas.width,
                    y: Math.random() * canvas.height,
                    speed: (Math.random() * 2 + 1) * (currentLevel === '3.000' ? 4 : currentLevel === '2.000' ? 2.5 : 1),
                    size: Math.random() * 3 + 1.5,
                    direction: Math.random() > 0.5 ? 1 : -1,
                    type: Math.floor(Math.random() * 3) // 0: Terrestre/Urbano, 1: Ar/Mar, 2: Espaço
                });
            }
        }

        function animateCanvas() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // DESENHAR PLANO DE FUNDO DE ACORDO COM O NÍVEL
            if (currentLevel === '0.732') {
                // Desenhar linhas de rodovias e rotas
                ctx.strokeStyle = 'rgba(30, 41, 59, 0.6)';
                ctx.lineWidth = 1;
                ctx.beginPath();
                ctx.moveTo(0, canvas.height * 0.7); ctx.lineTo(canvas.width, canvas.height * 0.7);
                ctx.moveTo(0, canvas.height * 0.4); ctx.lineTo(canvas.width, canvas.height * 0.4);
                ctx.stroke();
            } else if (currentLevel === '1.000') {
                // Desenhar linhas de Elevador Espacial e Maglev
                ctx.strokeStyle = 'rgba(16, 185, 129, 0.2)';
                ctx.lineWidth = 2;
                ctx.beginPath();
                ctx.moveTo(canvas.width * 0.5, 0); ctx.lineTo(canvas.width * 0.5, canvas.height);
                ctx.stroke();
            } else if (currentLevel === '2.000') {
                // Sol central e órbitas do Enxame de Dyson
                ctx.fillStyle = 'rgba(245, 158, 11, 0.15)';
                ctx.beginPath();
                ctx.arc(canvas.width * 0.5, canvas.height * 0.5, 45, 0, Math.PI * 2);
                ctx.fill();
            } else if (currentLevel === '3.000') {
                // Núcleo de Buraco Negro / Sagitário A*
                ctx.fillStyle = 'rgba(168, 85, 247, 0.2)';
                ctx.beginPath();
                ctx.arc(canvas.width * 0.5, canvas.height * 0.5, 30, 0, Math.PI * 2);
                ctx.fill();
            }

            // MOVER E DESENHAR PARTÍCULAS / VEÍCULOS
            particles.forEach(p => {
                p.x += p.speed * p.direction;

                if (p.x > canvas.width) p.x = 0;
                if (p.x < 0) p.x = canvas.width;

                ctx.beginPath();
                ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);

                if (currentLevel === '0.732') {
                    ctx.fillStyle = p.type === 0 ? '#06b6d4' : p.type === 1 ? '#f59e0b' : '#38bdf8';
                } else if (currentLevel === '1.000') {
                    ctx.fillStyle = p.type === 0 ? '#10b981' : p.type === 1 ? '#34d399' : '#059669';
                } else if (currentLevel === '2.000') {
                    ctx.fillStyle = p.type === 0 ? '#f59e0b' : p.type === 1 ? '#fbbf24' : '#d97706';
                } else {
                    ctx.fillStyle = p.type === 0 ? '#a855f7' : p.type === 1 ? '#c084fc' : '#e879f9';
                }

                ctx.fill();
            });

            requestAnimationFrame(animateCanvas);
        }
    </script>
</body>
</html>
