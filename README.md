# Atividade-06-a



<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <title>Consulta Temperatura - OpenWeatherMap</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; }
    input, button { padding: 8px; margin-top: 10px; }
    #resultado { margin-top: 20px; font-size: 1.2em; }
  </style>
</head>
<body>

  <h1>Consultar Temperatura de uma Cidade</h1>

  <label for="cidade">Digite o nome da cidade:</label><br/>
  <input type="text" id="cidade" placeholder="Ex: São Paulo" />
  <button onclick="buscarTemperatura()">Buscar temperatura</button>

  <div id="resultado"></div>

  <script>
    const openWeatherKey = "5515d3e5a8b0dd17c4711b7a03f1890b"; 
    const openWeatherURL = "https://api.openweathermap.org/data/2.5/weather?appid={API key}";

    const inputCidade = document.getElementById("cidade");
    const divResultado = document.getElementById("resultado");

    function buscarTemperatura() {
      const cidade = inputCidade.value.trim();
      if (!cidade) {
        divResultado.textContent = "Por favor, digite o nome de uma cidade.";
        return;
      }

      divResultado.textContent = "Buscando temperatura...";

      // Monta a URL correta com os parâmetros necessários
      const url = `${openWeatherURL}?q=${encodeURIComponent(cidade)},BR&units=metric&lang=pt_br&appid=${openWeatherKey}`;

      fetch(url)
        .then(res => {
          if (!res.ok) throw new Error("Cidade não encontrada ou erro na API de clima.");
          return res.json();
        })
        .then(data => {
          const temp = data.main.temp;
          divResultado.textContent = `Temperatura atual em ${cidade}: ${temp.toFixed(1)} °C`;
        })
        .catch(err => {
          divResultado.textContent = `Erro: ${err.message}`;
        });
    }
  </script>

</body>
</html>

