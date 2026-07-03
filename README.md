<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Trueque Inteligente</title>
  <link rel="stylesheet" href="style.css">
</head>

<body>

  <header>
    <h1>Trueque Inteligente</h1>
    <p>Intercambia, vende y encuentra lo que necesitas</p>
  </header>

  <section class="formulario">
    <h2>Publicar producto</h2>

    <input type="text" id="nombre" placeholder="Nombre del producto">
    <input type="text" id="descripcion" placeholder="Descripción">
    <button onclick="agregarProducto()">Publicar</button>
  </section>

  <section class="productos">
    <h2>Productos publicados</h2>
    <div id="lista"></div>
  </section>

  <script src="app.js"></script>
</body>
</html>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  background: #f4f4f4;
}

header {
  background: #2c3e50;
  color: white;
  padding: 20px;
  text-align: center;
}

.formulario {
  background: white;
  padding: 20px;
  margin: 20px;
  border-radius: 10px;
}

input {
  display: block;
  width: 100%;
  margin: 10px 0;
  padding: 10px;
}

button {
  padding: 10px;
  background: #27ae60;
  color: white;
  border: none;
  cursor: pointer;
}

button:hover {
  background: #219150;
}

.productos {
  margin: 20px;
}

.card {
  background: white;
  padding: 10px;
  margin: 10px 0;
  border-radius: 10px;
}function agregarProducto() {
  let nombre = document.getElementById("nombre").value;
  let descripcion = document.getElementById("descripcion").value;

  if (nombre === "" || descripcion === "") {
    alert("Completa todos los campos");
    return;
  }

  let contenedor = document.getElementById("lista");

  let card = document.createElement("div");
  card.classList.add("card");

  card.innerHTML = `
    <h3>${nombre}</h3>
    <p>${descripcion}</p>
  `;

  contenedor.appendChild(card);

  document.getElementById("nombre").value = "";
  document.getElementById("descripcion").value = "";
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Trueque Inteligente</title>
</head>

<body>

<h2>Registro / Login</h2>

<input id="email" placeholder="Email">
<input id="password" placeholder="Contraseña">

<button onclick="registrar()">Registrarse</button>
<button onclick="login()">Iniciar sesión</button>

<hr>

<h2>Publicar producto</h2>

<input id="nombre" placeholder="Producto">
<input id="desc" placeholder="Descripción">

<button onclick="publicar()">Publicar</button>

<h2>Productos</h2>
<div id="lista"></div>

<!-- FIREBASE -->
<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
import { 
  getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword 
} from "https://www.gstatic.com/firebasejs/10.12.0/firebase-auth.js";

import {
  getFirestore, collection, addDoc, getDocs
} from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";

/* 🔥 TU CONFIG AQUÍ */
const firebaseConfig = {
  apiKey: "TU_API_KEY",
  authDomain: "TU_AUTH_DOMAIN",
  projectId: "TU_PROJECT_ID",
  storageBucket: "TU_BUCKET",
  messagingSenderId: "TU_SENDER_ID",
  appId: "TU_APP_ID"
};

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);

/* 👤 AUTH */
window.registrar = async function () {
  let email = document.getElementById("email").value;
  let pass = document.getElementById("password").value;

  await createUserWithEmailAndPassword(auth, email, pass);
  alert("Usuario creado");
}

window.login = async function () {
  let email = document.getElementById("email").value;
  let pass = document.getElementById("password").value;

  await signInWithEmailAndPassword(auth, email, pass);
  alert("Sesión iniciada");
}

/* 📦 PRODUCTOS */
window.publicar = async function () {
  let nombre = document.getElementById("nombre").value;
  let desc = document.getElementById("desc").value;

  await addDoc(collection(db, "productos"), {
    nombre,
    desc
  });

  alert("Producto publicado");
  mostrar();
}

window.mostrar = async function () {
  let lista = document.getElementById("lista");
  lista.innerHTML = "";

  let querySnapshot = await getDocs(collection(db, "productos"));

  querySnapshot.forEach((doc) => {
    let p = doc.data();

    let div = document.createElement("div");
    div.innerHTML = `
      <h3>${p.nombre}</h3>
      <p>${p.desc}</p>
      <hr>
    `;

    lista.appendChild(div);
  });
}

mostrar();

</script>

</body>
</html>
