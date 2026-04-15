# Barbearias-alem-o-
Agendamentos de corte 
<!DOCTYPE html><html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Barbearia - Agendamento</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #0f0f0f;
      color: #fff;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }.container {
  background: #1e1e1e;
  padding: 25px;
  border-radius: 12px;
  width: 320px;
  text-align: center;
  box-shadow: 0 0 20px rgba(0,0,0,0.5);
}

h1 {
  margin-bottom: 15px;
}

input {
  width: 100%;
  padding: 10px;
  margin: 10px 0;
  border-radius: 6px;
  border: none;
}

.horario {
  padding: 10px;
  margin: 5px 0;
  background: #333;
  border-radius: 6px;
  cursor: pointer;
}

.ocupado {
  background: #555;
  text-decoration: line-through;
  cursor: not-allowed;
}

.selecionado {
  background: #00c853 !important;
}

button {
  width: 100%;
  padding: 12px;
  margin-top: 10px;
  border-radius: 6px;
  border: none;
  background: #00c853;
  color: white;
  font-weight: bold;
  cursor: pointer;
}

  </style>
</head>
<body><div class="container">
  <h1>Agendar Corte</h1>  <input type="text" id="nome" placeholder="Seu nome">  <div id="horarios"></div><button onclick="agendar()">Agendar via WhatsApp</button>

</div><script>
  const horarios = [
    "12:00","12:30","13:00","13:30",
    "14:00","14:30","15:00","15:30",
    "16:00","16:30","17:00"
  ];

  let selecionado = null;

  function render() {
    const container = document.getElementById("horarios");
    container.innerHTML = "";

    horarios.forEach((hora, i) => {
      const div = document.createElement("div");
      div.className = "horario";
      div.innerText = hora;

      if (localStorage.getItem(hora)) {
        div.classList.add("ocupado");
      }

      if (selecionado === i) {
        div.classList.add("selecionado");
      }

      div.onclick = () => {
        if (div.classList.contains("ocupado")) return;
        selecionado = i;
        render();
      };

      container.appendChild(div);
    });
  }

  function agendar() {
    const nome = document.getElementById("nome").value;

    if (!nome) {
      alert("Digite seu nome!");
      return;
    }

    if (selecionado === null) {
      alert("Escolha um horário!");
      return;
    }

    const hora = horarios[selecionado];

    localStorage.setItem(hora, nome);

    const mensagem = `Olá, meu nome é ${nome} e quero agendar um corte às ${hora}`;

    const telefone = "5511999999999"; // TROQUE PELO SEU NÚMERO

    window.open(`https://wa.me/${telefone}?text=${encodeURIComponent(mensagem)}`);

    render();
  }

  render();
</script></body>
</html>
