<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>🌿 App Anti-Crisis</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="manifest" href="manifest.json">

  <script>
    if ("serviceWorker" in navigator) {
      navigator.serviceWorker.register("sw.js")
        .then(reg => console.log("Service Worker registrado:", reg))
        .catch(err => console.error("Error en SW:", err));
    }
  </script>

  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(-45deg, #e0f7fa, #e1bee7, #bbdefb, #c8e6c9);
      background-size: 400% 400%;
      animation: gradientBG 15s ease infinite;
      margin: 0;
      padding: 0;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: flex-start;
    }

    @keyframes gradientBG {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    #pantalla {
      margin-top: 30px;
      background: rgba(255, 255, 255, 0.85);
      border-radius: 15px;
      padding: 20px;
      max-width: 500px;
      width: 90%;
      box-shadow: 0 4px 12px rgba(0,0,0,0.3);
      text-align: center;
    }

    button {
      display: block;
      width: 90%;
      max-width: 300px;
      margin: 10px auto;
      padding: 12px 18px;
      font-size: 16px;
      border-radius: 10px;
      border: none;
      background: #3aafa9;
      color: white;
      cursor: pointer;
      transition: transform 0.2s, background 0.3s;
    }

    button:hover {
      background: #2b7a78;
      transform: scale(1.05);
    }

    textarea {
      width: 90%;
      max-width: 400px;
      height: 80px;
      padding: 10px;
      border-radius: 8px;
      border: 1px solid #aaa;
      margin: 10px 0;
    }

    img {
      width: 90%;
      max-width: 400px;
      border-radius: 10px;
      margin-top: 10px;
    }
  </style>
</head>
<body>
  <div id="pantalla"></div>

  <script>
    const pantalla = document.getElementById("pantalla");

    // === Inicio ===
    function inicio() {
      pantalla.innerHTML = `
        <h1>🌿 App Anti-Crisis 🌿</h1>
        <button onclick="mostrarOpciones()">🚨 Tengo una crisis</button>
        <button onclick="mostrarMeSientoMal()">🌙 Me siento mal</button>
      `;
    }

    // === CRISIS ===
    function mostrarOpciones() {
      pantalla.innerHTML = `
        <h2>Respira, estás a salvo 🌸</h2>
        <button onclick="respiracion()">🌬 Ejercicio de respiración</button>
        <button onclick="grounding()">🌱 Grounding 5 sentidos</button>
        <button onclick="frasesPositivas()">💙 Frases positivas</button>
        <button onclick="distraccion()">🎮 Distracción rápida</button>
        <button onclick="audioEjercicio()">🎧 Relajación con música</button>
        <button onclick="contactoRapido()">📞 Contacto rápido</button>
        <button onclick="inicio()">⬅ Volver</button>
      `;
    }

    function respiracion() {
      pantalla.innerHTML = `
        <h2>🌬 Respiración 4-4-6</h2>
        <p>Inhala 4s, mantén 4s, exhala 6s</p>
        <button onclick="mostrarOpciones()">⬅ Volver</button>
      `;
    }

    function grounding() {
      pantalla.innerHTML = `
        <h2>🌱 Grounding 5 sentidos</h2>
        <ul style="text-align:left">
          <li>5 cosas que ves</li>
          <li>4 cosas que tocas</li>
          <li>3 cosas que oyes</li>
          <li>2 cosas que hueles</li>
          <li>1 cosa que saboreas</li>
        </ul>
        <button onclick="mostrarOpciones()">⬅ Volver</button>
      `;
    }

    function frasesPositivas() {
      const frases = [
        "Esto también pasará 💙",
        "Soy más fuerte de lo que pienso ✨",
        "Un paso a la vez 🌿",
        "Merezco estar en paz 💫"
      ];
      const aleatoria = frases[Math.floor(Math.random()*frases.length)];
      pantalla.innerHTML = `
        <h2>💙 Frase positiva</h2>
        <p>${aleatoria}</p>
        <button onclick="frasesPositivas()">Otra</button>
        <button onclick="mostrarOpciones()">⬅ Volver</button>
      `;
    }

    function distraccion() {
      pantalla.innerHTML = `
        <h2>🎮 Juego rápido</h2>
        <p>Cuenta hacia atrás desde 50 en múltiplos de 3</p>
        <button onclick="mostrarOpciones()">⬅ Volver</button>
      `;
    }

    // === Música Crisis (con guardado) ===
    function audioEjercicio() {
      let musicaCrisis = localStorage.getItem("musicaCrisis");
      pantalla.innerHTML = `
        <h2>🎧 Relajación</h2>
        <audio id="playerCrisis" controls autoplay>
          ${musicaCrisis ? `<source src="${musicaCrisis}" type="audio/mpeg">`
                         : `<source src="sounds/lluvia.mp3" type="audio/mpeg">`}
        </audio>
        <h3>📂 Sube tu propia música</h3>
        <input type="file" accept="audio/*" onchange="cargarMusicaCrisis(event)">
        <br>
        <button onclick="mostrarOpciones()">⬅ Volver</button>
      `;
    }

    function cargarMusicaCrisis(event) {
      const archivo = event.target.files[0];
      if (archivo) {
        const reader = new FileReader();
        reader.onload = function(e) {
          localStorage.setItem("musicaCrisis", e.target.result);
          document.getElementById("playerCrisis").src = e.target.result;
          document.getElementById("playerCrisis").play();
        };
        reader.readAsDataURL(archivo);
      }
    }

    function contactoRapido() {
      pantalla.innerHTML = `
        <h2>📞 Contacto rápido</h2>
        <button onclick="window.location.href='tel:105'">🚑 Emergencias</button>
        <button onclick="window.location.href='tel:100'">📞 Línea 100</button>
        <button onclick="window.location.href='mailto:apoyo@email.com'">📧 Enviar correo</button>
        <button onclick="mostrarOpciones()">⬅ Volver</button>
      `;
    }

    // === ME SIENTO MAL ===
    function mostrarMeSientoMal() {
      pantalla.innerHTML = `
        <h2>🌙 Me siento mal</h2>
        <button onclick="musica()">🎶 Música relajante</button>
        <button onclick="afirmaciones()">📖 Afirmaciones</button>
        <button onclick="escribirPensamientos()">✍️ Mis notas</button>
        <button onclick="imagenes()">🌄 Imágenes tranquilas</button>
        <button onclick="rutina()">📅 Autocuidado rápido</button>
        <button onclick="inicio()">⬅ Volver</button>
      `;
    }

    // === Música Relax (con guardado) ===
    function musica() {
      let musicaGuardada = localStorage.getItem("musicaRelax");
      pantalla.innerHTML = `
        <h2>🎶 Música</h2>
        <audio id="player" controls autoplay>
          ${musicaGuardada ? `<source src="${musicaGuardada}" type="audio/mpeg">`
                           : `<source src="sounds/bosque.mp3" type="audio/mpeg">`}
        </audio>
        <h3>📂 Sube tu propia música</h3>
        <input type="file" accept="audio/*" onchange="cargarMusica(event)">
        <button onclick="mostrarMeSientoMal()">⬅ Volver</button>
      `;
    }

    function cargarMusica(event) {
      const archivo = event.target.files[0];
      if (archivo) {
        const reader = new FileReader();
        reader.onload = function(e) {
          localStorage.setItem("musicaRelax", e.target.result);
          document.getElementById("player").src = e.target.result;
          document.getElementById("player").play();
        };
        reader.readAsDataURL(archivo);
      }
    }

    // === Afirmaciones ===
    function afirmaciones() {
      const frases = [
        "Hoy me permito descansar 🌿",
        "Soy suficiente 💙",
        "Merezco calma ✨",
        "Mi valor no depende de mi ánimo 🌸"
      ];
      const aleatoria = frases[Math.floor(Math.random()*frases.length)];
      pantalla.innerHTML = `
        <h2>📖 Afirmación</h2>
        <p>${aleatoria}</p>
        <button onclick="afirmaciones()">Otra</button>
        <button onclick="mostrarMeSientoMal()">⬅ Volver</button>
      `;
    }

    // === Notas ===
    function escribirPensamientos() {
      let notas = JSON.parse(localStorage.getItem("notas")) || [];
      let lista = notas.map((n,i)=>`<li>${n}</li>`).join("");
      pantalla.innerHTML = `
        <h2>✍️ Mis notas</h2>
        <textarea id="nota"></textarea>
        <button onclick="guardarNota()">💾 Guardar</button>
        <button onclick="borrarNotas()">🗑 Borrar todo</button>
        <button onclick="mostrarMeSientoMal()">⬅ Volver</button>
        <hr>
        <ul style="text-align:left">${lista || "<i>No hay notas</i>"}</ul>
      `;
    }

    function guardarNota() {
      let texto = document.getElementById("nota").value.trim();
      if (texto) {
        let notas = JSON.parse(localStorage.getItem("notas")) || [];
        notas.push(texto);
        localStorage.setItem("notas", JSON.stringify(notas));
        escribirPensamientos();
      } else {
        alert("✍️ Escribe algo");
      }
    }

    function borrarNotas() {
      if (confirm("¿Seguro?")) {
        localStorage.removeItem("notas");
        escribirPensamientos();
      }
    }

    // === Imágenes ===
    function imagenes() {
      const imgs = ["imagenes/paisaje1.jpg","imagenes/paisaje2.jpg","imagenes/paisaje3.jpg"];
      const random = imgs[Math.floor(Math.random()*imgs.length)];
      pantalla.innerHTML = `
        <h2>🌄 Imagen tranquila</h2>
        <img src="${random}" alt="Paisaje">
        <button onclick="imagenes()">Otra</button>
        <button onclick="mostrarMeSientoMal()">⬅ Volver</button>
      `;
    }

    // === Rutina ===
    function rutina() {
      pantalla.innerHTML = `
        <h2>📅 Autocuidado</h2>
        <ul style="text-align:left">
          <li>💧 Bebe agua</li>
          <li>🤸 Estírate</li>
          <li>🌬 Respira 3 veces</li>
          <li>🚶 Da una vuelta</li>
        </ul>
        <button onclick="mostrarMeSientoMal()">⬅ Volver</button>
      `;
    }

    // Lanzar inicio al cargar
    inicio();
  </script>
</body>
</html>

