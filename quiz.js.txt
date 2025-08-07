const perguntas = [
  {
    pergunta: "Quando o coração do embrião começa a bater?",
    opcoes: ["1ª semana", "2ª semana", "3ª semana", "4ª semana"],
    correta: 2,
    explicacao: "O coração começa a bater por volta do 22º dia (início da 4ª semana)."
  },
  {
    pergunta: "O que é o tubo neural?",
    opcoes: ["Futuro cérebro e medula", "Sistema digestivo", "Coração", "Pulmão"],
    correta: 0,
    explicacao: "O tubo neural dará origem ao cérebro e à medula espinhal."
  },
  {
    pergunta: "Tamanho do embrião ao fim da 4ª semana?",
    opcoes: ["1 mm", "5 mm", "10 cm", "2 cm"],
    correta: 1,
    explicacao: "O embrião mede cerca de 4 a 5 mm ao fim da 4ª semana."
  },
  {
    pergunta: "Qual sistema começa a funcionar primeiro?",
    opcoes: ["Digestivo", "Respiratório", "Circulatório", "Nervoso"],
    correta: 2,
    explicacao: "O sistema circulatório é o primeiro a funcionar no embrião."
  },
  {
    pergunta: "O que são os somitos?",
    opcoes: ["Células sanguíneas", "Futuros órgãos", "Futuros ossos e músculos", "Glândulas"],
    correta: 2,
    explicacao: "Os somitos originam músculos, vértebras e partes da pele."
  },
  {
    pergunta: "Quando o tubo neural se fecha completamente?",
    opcoes: ["1ª semana", "2ª semana", "3ª semana", "4ª semana"],
    correta: 3,
    explicacao: "O tubo neural se fecha totalmente por volta do final da 4ª semana."
  },
  {
    pergunta: "O embrião já tem olhos visíveis na 4ª semana?",
    opcoes: ["Sim", "Não"],
    correta: 0,
    explicacao: "Sim, aparecem os esboços dos olhos e ouvidos."
  },
  {
    pergunta: "Como os hormônios maternos afetam o embrião?",
    opcoes: ["Aceleram o desenvolvimento", "Interrompem o crescimento", "Não afetam", "Destroem células"],
    correta: 0,
    explicacao: "Hormônios maternos como o HCG ajudam a manter o desenvolvimento."
  },
  {
    pergunta: "Qual dessas estruturas já começa a se formar?",
    opcoes: ["Intestino", "Pulmões", "Cabelos", "Dentes"],
    correta: 0,
    explicacao: "O intestino primitivo já começa a se formar na 4ª semana."
  },
  {
    pergunta: "O embrião pode se mover nessa fase?",
    opcoes: ["Sim, involuntariamente", "Não", "Apenas com estímulos", "Já anda"],
    correta: 0,
    explicacao: "Pequenos movimentos involuntários já podem ocorrer no fim da 4ª semana."
  }
];

let indice = 0;
let pontuacao = 0;

const perguntaEl = document.getElementById('pergunta');
const opcoesEl = document.getElementById('opcoes');
const feedbackEl = document.getElementById('feedback');
const progressoEl = document.getElementById('progresso');
const btnProxima = document.getElementById('proxima');
const resultadoEl = document.getElementById('resultado');
const pontuacaoFinalEl = document.getElementById('pontuacao-final');

const somAcerto = new Howl({ src: ['audios/acerto.mp3'] });
const somErro = new Howl({ src: ['audios/erro.mp3'] });

function carregarPergunta() {
  const atual = perguntas[indice];
  perguntaEl.textContent = atual.pergunta;
  opcoesEl.innerHTML = "";
  feedbackEl.textContent = "";

  atual.opcoes.forEach((opcao, i) => {
    const li = document.createElement("li");
    li.textContent = opcao;
    li.onclick = () => verificarResposta(i);
    opcoesEl.appendChild(li);
  });

  progressoEl.textContent = `Pergunta ${indice + 1} de ${perguntas.length}`;
  btnProxima.style.display = "none";
}

function verificarResposta(resposta) {
  const correta = perguntas[indice].correta;

  if (resposta === correta) {
    feedbackEl.textContent = "✅ Correto! " + perguntas[indice].explicacao;
    somAcerto.play();
    pontuacao++;
  } else {
    feedbackEl.textContent = "❌ Errado. " + perguntas[indice].explicacao;
    somErro.play();
  }

  Array.from(opcoesEl.children).forEach((li, i) => {
    li.classList.add(i === correta ? "certa" : i === resposta ? "errada" : "desativada");
    li.onclick = null;
  });

  btnProxima.style.display = "block";
}

btnProxima.onclick = () => {
  indice++;
  if (indice < perguntas.length) {
    carregarPergunta();
  } else {
    mostrarResultado();
  }
};

function mostrarResultado() {
  document.getElementById('quiz-container').style.display = "none";
  resultadoEl.style.display = "block";
  pontuacaoFinalEl.textContent = `Você acertou ${pontuacao} de ${perguntas.length} perguntas!`;

  // confete 🎉
  confetti({
    particleCount: 150,
    spread: 100,
    origin: { y: 0.6 }
  });
}

carregarPergunta();
