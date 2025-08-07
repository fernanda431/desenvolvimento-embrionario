function toggleMenu() {
  const menu = document.getElementById('sideMenu');
  menu.style.display = menu.style.display === 'block' ? 'none' : 'block';
}

// Frases rotativas
const frases = [
  "O coração começa a bater por volta da 3ª semana!",
  "O embrião mede apenas milímetros, mas já está em formação ativa.",
  "O tubo neural começa a se fechar nessa fase!",
  "Placenta e cordão umbilical começam a se desenvolver.",
  "Células-tronco estão a todo vapor formando tecidos!",
  "Até o fim da 4ª semana, o sistema nervoso já mostra atividade.",
  "Patologias como anencefalia surgem por falhas no tubo neural.",
  "A implantação ocorre na 2ª semana — o embrião 'gruda' no útero.",
  "O desenvolvimento depende de sinais genéticos precisos.",
  "Qualquer interferência nesse período pode causar malformações."
];

let fraseIndex = 0;
function trocarFrase() {
  const fraseElemento = document.getElementById("fraseCuriosidade");
  fraseElemento.textContent = frases[fraseIndex];
  fraseIndex = (fraseIndex + 1) % frases.length;
}
setInterval(trocarFrase, 4000);
window.onload = trocarFrase;
