<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <title>Cachorros com Imagens no HTML</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; }
    label, select, button { display: block; margin: 10px 0; }
    img { max-width: 300px; display: none; margin-top: 10px; }
    .info { margin-top: 20px; }
  </style>
</head>
<body>

  <h1>Escolha seu cachorro</h1>

  <label for="raca">Raça:</label>
  <select id="raca"></select>

  <label for="cor">Cor:</label>
  <select id="cor"></select>

  <button onclick="criarCachorro()">Ver Cachorro</button>

  <div id="resultado" class="info"></div>

  <img id="img-bernesemountain" src="img/OIP-360x286.png" alt="Labrador">
  <img id="img-shitzu" src="img/shitzu.png" alt="Bulldog">
  <img id="img-pinscher" src="img/pinscher.webp" alt="Pastor Alemão">
  <img id="img-cocker" src="img/cocker-spaniel-english.png" alt="Poodle">

  <script>
    class Animal {
      constructor(patas, olhos) {
        this.patas = patas;
        this.olhos = olhos;
      }
    }

    class Cachorro extends Animal {
      constructor(patas, olhos, raca, cor) {
        super(patas, olhos);
        this.raca = raca;
        this.cor = cor;
      }
    }

    const racas = {
      bernesemountain: {
        nome: "Bernese Mountain",
        descricao: "Amigável, energético e ótimo com crianças.",
        cores: ["Marrom e preto"]
      },
      shitzu: {
        nome: "Shitzu",
        descricao: "Calmo, brincalhão e muito afetuoso.",
        cores: ["Preto e Branco", "Marrom e Branco"]
      },
      Pinscher: {
        nome: "pinscher",
        descricao: "Temperamental, arisco e corajoso.",
        cores: ["Preto e Marrom", "Preto", "Marrom"]
      },
      cocker: {
        nome: "Cocker",
        descricao: "Elegante, fragil e preguiçoso.",
        cores: ["Caramelo", "Marrom", "Cinza", "Cinza e Branco", "Marrom e Branco"]
      }
    };

    const selectRaca = document.getElementById("raca");
    const selectCor = document.getElementById("cor");
    const resultado = document.getElementById("resultado");

    window.onload = () => {
      for (let chave in racas) {
        const opt = document.createElement("option");
        opt.value = chave;
        opt.textContent = racas[chave].nome;
        selectRaca.appendChild(opt);
      }

      atualizarCores();
      selectRaca.addEventListener("change", atualizarCores);
    };

    function atualizarCores() {
      const racaSelecionada = selectRaca.value;
      const cores = racas[racaSelecionada].cores;

      selectCor.innerHTML = "";
      cores.forEach(cor => {
        const opt = document.createElement("option");
        opt.value = cor;
        opt.textContent = cor;
        selectCor.appendChild(opt);
      });
    }

    function esconderTodasImagens() {
      document.querySelectorAll("img[id^='img-']").forEach(img => {
        img.style.display = "none";
      });
    }

    function criarCachorro() {
      const racaKey = selectRaca.value;
      const cor = selectCor.value;
      const dados = racas[racaKey];

      const cachorro = new Cachorro(4, 2, dados.nome, cor);

      resultado.innerHTML = `
        <h2>${cachorro.raca}</h2>
        <p><strong>Cor:</strong> ${cachorro.cor}</p>
        <p><strong>Patas:</strong> ${cachorro.patas} | <strong>Olhos:</strong> ${cachorro.olhos}</p>
        <p><strong>Descrição:</strong> ${dados.descricao}</p>
      `;

      // Mostrar imagem correta
      esconderTodasImagens();
      document.getElementById(`img-${racaKey}`).style.display = "block";
    }
  </script>
</body>
</html>
