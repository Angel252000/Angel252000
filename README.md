
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
      background-color: #000000;
      color: #00ff00;
      font-family: 'Courier New', Courier, monospace;
      font-size: 1rem;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
      overflow: hidden;
    }
    .terminal {
      width: 95%;
      max-width: 900px;
      height: 90vh;
      background-color: #101010;
      border: 2px solid #00ff00;
      padding: 2rem;
      box-shadow: 0 0 20px #00ff00;
      overflow-y: auto;
      border-radius: 8px;
    }
    .line {
      display: block;
      margin-bottom: 0.7rem;
      white-space: pre-wrap;
    }
    .prompt::before {
      content: 'angel252000@github:~$ ';
      color: #00ff00;
    }
    .blinking-cursor {
      display: inline-block;
      width: 10px;
      height: 1.2rem;
      background-color: #00ff00;
      animation: blink 1s step-start infinite;
      margin-left: 4px;
      vertical-align: bottom;
    }
    @keyframes blink {
      50% { opacity: 0; }
    }
  </style>
</head>
<body>
  <div class="terminal" id="terminal"></div>

  <script>
    const terminal = document.getElementById('terminal');
    const commands = [
      "whoami",
      "👨‍💻 Ángel Amaya — Estudiante de Ingeniería en Sistemas en UNADECA",

      "echo \"🎯 Pasiones\"",
      "💡 Me encanta programar, diseñar interfaces intuitivas y explorar APIs modernas.",

      "echo \"🧰 Tecnologías\"",
      "🚀 React Native, FastAPI, Python, MySQL, Figma, Git, GitHub",

      "projects list",
      "📱 MusicApp - Reproductor moderno con autenticación y modo oscuro",
      "📊 HorasBeca - Gestor con control de asistencia y pagos automáticos",
      "🔐 AuthAPI - Microservicio con JWT y OAuth",

      "stats",
      "📈 240+ commits en 2024 | 18 repos públicos | 8 proyectos colaborativos",

      "social",
      "🔗 LinkedIn: linkedin.com/in/angelamaya",
      "📧 Correo: angelamaya@email.com",

      "exit",
      "👋 ¡Gracias por visitar mi terminal! ¡Nos vemos en el próximo commit!"
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

      const current = commands[i];
      let interval = setInterval(() => {
        if (char < current.length) {
          line.textContent += current[char++];
        } else {
          clearInterval(interval);
          line.innerHTML += '<span class="blinking-cursor"></span>';
          i++;
          char = 0;
          isCommand = !isCommand;
          setTimeout(() => {
            line.querySelector('.blinking-cursor').remove();
            typeLine();
          }, 600);
        }
      }, 35);
    }

    typeLine();
  </script>
</body>
</html>
