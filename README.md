<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>CHECKDIGITO – Codificador Hexadecimal</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #eafaf1;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
    }
    .container {
      background: white;
      border-radius: 12px;
      padding: 30px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
      width: 100%;
      max-width: 400px;
      text-align: center;
    }
    h1 {
      margin-top: 0;
      color: #2d7a3e;
    }
    input[type="text"] {
      width: 100%;
      padding: 10px;
      margin-bottom: 15px;
      font-size: 1rem;
      border: 2px solid #a3d9a5;
      border-radius: 6px;
    }
    button {
      padding: 10px 15px;
      font-size: 1rem;
      background-color: #2d7a3e;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      margin: 5px 0;
      width: 100%;
    }
    .output {
      margin-top: 20px;
      font-weight: bold;
      word-break: break-word;
      color: #2d7a3e;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>CHECKDIGITO</h1>
    <input type="text" id="inputText" placeholder="Digite 7 caracteres (ex: C29HQ36)" maxlength="7">
    <button onclick="codificar()">Codificar</button>
    <button onclick="copiar()">Copiar Código</button>
    <div class="output" id="output"></div>
  </div>

  <script>
    const shifts = [12, 1, 9, 3, 15, 13, 11];

    function codificar() {
      const input = document.getElementById("inputText").value;
      const outputDiv = document.getElementById("output");
      if (input.length !== 7) {
        outputDiv.innerText = "Erro: Digite exatamente 7 caracteres.";
        return;
      }
      let resultado = "";
      for (let i = 0; i < 7; i++) {
        const ascii = input[i].charCodeAt(0);
        const deslocado = ascii + shifts[i];
        resultado += deslocado.toString(16).toUpperCase().padStart(2, '0');
      }
      outputDiv.innerText = "Código Hex: " + resultado;
    }

    function copiar() {
      const text = document.getElementById("output").innerText.replace("Código Hex: ", "");
      if (!text) return;
      navigator.clipboard.writeText(text).then(() => {
        alert("🔓 Código copiado: " + text);
      });
    }
  </script>
</body>
</html>
