<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Corretor de Elite | Imóveis de Alto Padrão</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Montserrat', sans-serif; }
        .gold-gradient { background: linear-gradient(135deg, #D4AF37 0%, #B8860B 100%); }
        .navy-bg { background-color: #0F172A; }
        .sticky-bar { backdrop-filter: blur(10px); background: rgba(15, 23, 42, 0.8); }
    </style>
</head>
<body class="bg-gray-50 text-slate-900">

    <header class="navy-bg text-white py-16 px-6 md:px-20 lg:flex items-center justify-between">
        <div class="lg:w-1/2 space-y-6">
            <h2 class="text-gold-500 uppercase tracking-widest text-sm font-bold text-[#D4AF37]">Especialista Imobiliário</h2>
            <h1 class="text-4xl md:text-6xl font-bold">Ricardo Silva</h1>
            <p class="text-gray-300 text-lg leading-relaxed">
                Especialista em imóveis de alto padrão na **Zona Sul e Centro**. 
                Com mais de 10 anos de mercado, foco em curadoria exclusiva para quem busca morar bem ou investir com segurança.
            </p>
            <div class="flex gap-4">
                <span class="bg-slate-800 px-4 py-2 rounded-full text-sm font-semibold">📍 São Paulo, SP</span>
                <span class="bg-slate-800 px-4 py-2 rounded-full text-sm font-semibold">🏠 Venda & Avaliação</span>
            </div>
        </div>
        
        <div class="lg:w-1/3 mt-10 lg:mt-0 relative">
            <div class="absolute -inset-4 gold-gradient rounded-xl blur opacity-30"></div>
            <img src="https://images.unsplash.com/photo-1560250097-0b93528c311a?auto=format&fit=crop&q=80&w=400" 
                 alt="Corretor" class="relative rounded-xl border-2 border-[#D4AF37] grayscale hover:grayscale-0 transition duration-500">
        </div>
    </header>

    <main class="max-w-7xl mx-auto py-16 px-6">
        <div class="flex items-center justify-between mb-10">
            <h2 class="text-3xl font-bold italic">Oportunidades Selecionadas</h2>
            <div class="h-1 w-24 gold-gradient"></div>
        </div>

        <div id="imoveis-container" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            <div id="loading" class="col-span-full flex flex-col items-center py-20">
                <i data-lucide="loader-2" class="w-10 h-10 animate-spin text-[#D4AF37]"></i>
                <p class="mt-4 text-gray-500">Carregando as melhores ofertas...</p>
            </div>
        </div>
    </main>

    <div class="fixed bottom-6 left-1/2 -translate-x-1/2 z-50 w-[90%] md:w-auto">
        <div class="sticky-bar border border-slate-700 px-6 py-4 rounded-full shadow-2xl flex items-center justify-around gap-6 text-white">
            <a href="https://wa.me/5511999999999" target="_blank" class="hover:text-green-400 transition transform hover:scale-110">
                <i data-lucide="message-circle"></i>
            </a>
            <a href="mailto:contato@exemplo.com" class="hover:text-blue-400 transition transform hover:scale-110">
                <i data-lucide="mail"></i>
            </a>
            <a href="#" class="hover:text-sky-400 transition transform hover:scale-110">
                <i data-lucide="send"></i>
            </a>
            <div class="h-6 w-[1px] bg-slate-600"></div>
            <p class="hidden md:block text-xs font-bold tracking-tighter uppercase">Fale Comigo Agora</p>
        </div>
    </div>

    <script>
        // Inicializa Ícones
        lucide.createIcons();

        // Lógica de Integração com o JSON
        async function carregarImoveis() {
            const container = document.getElementById('imoveis-container');
            const loader = document.getElementById('loading');

            try {
                // Tenta carregar o arquivo gerado pelo Python
                const response = await fetch('imoveis.json');
                const data = await response.json();

                loader.style.display = 'none';

                data.forEach(imovel => {
                    const card = `
                        <div class="bg-white rounded-xl shadow-lg overflow-hidden group border border-gray-100 hover:border-[#D4AF37] transition duration-300">
                            <div class="relative overflow-hidden">
                                <img src="${imovel.imagem}" alt="${imovel.titulo}" class="w-full h-56 object-cover group-hover:scale-110 transition duration-500">
                                <div class="absolute top-4 right-4 bg-white/90 px-3 py-1 rounded-full font-bold text-sm text-slate-900 shadow-sm">
                                    ${imovel.preco}
                                </div>
                            </div>
                            <div class="p-6">
                                <h3 class="text-xl font-bold mb-3">${imovel.titulo}</h3>
                                <a href="${imovel.link}" target="_blank" class="block text-center w-full py-3 rounded-lg border-2 border-slate-900 font-bold hover:bg-slate-900 hover:text-white transition duration-200">
                                    Ver Detalhes
                                </a>
                            </div>
                        </div>
                    `;
                    container.innerHTML += card;
                });
            } catch (error) {
                console.error("Erro ao carregar JSON:", error);
                loader.innerHTML = "<p class='text-red-500'>Erro ao carregar imóveis. Verifique se o imoveis.json existe.</p>";
            }
        }

        carregarImoveis();
    </script>
</body>
</html>
