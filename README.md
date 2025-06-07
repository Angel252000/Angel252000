<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Terminal Retro - Ángel Amaya</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      background-color: #0f0f0f;
      color: #00ff00;
      font-family: 'Courier New', Courier, monospace;
      font-size: 1.1rem;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
    }
    .terminal {
      width: 90%;
      max-width: 800px;
      background-color: #000000;
      border: 2px solid #00ff00;
      padding: 2rem;
      box-shadow: 0 0 10px #00ff00;
      overflow-y: auto;
    }
    .line {
      display: block;
      margin-bottom: 0.5rem;
    }
    .prompt::before {
      content: 'angel252000@github:~$ ';
      color: #0f0;
    }
    .blinking-cursor {
      display: inline-block;
      width: 10px;
      background-color: #00ff00;
      animation: blink 1s step-start 0s infinite;
      margin-left: 5px;
    }
    @keyframes blink {
      50% {
        opacity: 0;
      }
    }
  </style>
</head>
<body>
  <div class="terminal" id="terminal"></div>

  <script>
    const terminal = document.getElementById('terminal');
    const commands = [
      "whoami",
      "👨‍💻 Ángel Amaya — Ing. en Sistemas",
      "skills",
      "🛠 React Native, FastAPI, Python, MySQL",
      "projects --top",
      "🚀 app-musica\n🧭 gestor-horas-beca\n🔐 api-auth-fastapi",
      "stats",
      "📊 34 commits este mes\n🔥 7 días de actividad continua",
      "exit",
      "Hasta luego, ¡sigue programando!"
    ];

    let i = 0;
    let char = 0;
    let isCommand = true;

    function typeLine() {
      if (i >= commands.length) return;

      const line = document.createElement('div');
      line.classList.add('line');
      if (isCommand) line.classList.add('prompt');
      terminal.appendChild(line);

      const currentCommand = commands[i];
      let interval = setInterval(() => {
        if (char < currentCommand.length) {
          line.textContent += currentCommand[char++];
        } else {
          clearInterval(interval);
          line.innerHTML += '<span class="blinking-cursor"></span>';
          i++;
          char = 0;
          isCommand = !isCommand;
          setTimeout(() => {
            line.querySelector('.blinking-cursor').remove();
            typeLine();
          }, 500);
        }
      }, 40);
    }

    typeLine();
  </script>
</body>
</html>
