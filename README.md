# emprendecontrol <!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>EmprendeControl PRO</title>

<style>
body { font-family: Arial; background: #f5f5f5; text-align: center; }
h1 { color: #6a0dad; }

.box {
    background: white;
    padding: 15px;
    margin: 10px auto;
    width: 90%;
    max-width: 350px;
    border-radius: 15px;
    box-shadow: 0 0 10px #ccc;
}

input, select, button {
    padding: 10px;
    margin: 5px;
    width: 90%;
}

button {
    background: #6a0dad;
    color: white;
    border: none;
}

li { text-align: left; margin: 10px 0; }
small { color: gray; }
</style>

</head>
<body>

<h1>📱 EmprendeControl PRO</h1>

<div class="box">
<h3>Registrar Venta</h3>

<input type="text" id="cliente" placeholder="Cliente">
<input type="number" id="monto" placeholder="Monto S/">

<select id="pago">
<option value="">Método de pago</option>
<option value="Crédito">Tarjeta Crédito</option>
<option value="Débito">Tarjeta Débito</option>
<option value="Yape">Yape</option>
<option value="Plin">Plin</option>
<option value="Efectivo">Efectivo</option>
</select>

<button onclick="agregar()">Guardar</button>
</div>

<div class="box">
<h3>Historial</h3>
<ul id="lista"></ul>
</div>

<div class="box">
<h3>Total: S/ <span id="total">0</span></h3>
</div>

<script>
let pedidos = JSON.parse(localStorage.getItem("pedidos")) || [];

function guardar() {
    localStorage.setItem("pedidos", JSON.stringify(pedidos));
}

function mostrar() {
    let lista = document.getElementById("lista");
    lista.innerHTML = "";
    let total = 0;

    pedidos.forEach((p, i) => {
        let item = document.createElement("li");

        item.innerHTML = `
        <b>${p.cliente}</b><br>
        💰 S/ ${p.monto}<br>
        💳 ${p.pago}<br>
        🕒 ${p.fecha}<br>
        <button onclick="eliminar(${i})">Eliminar</button>
        `;

        lista.appendChild(item);
        total += p.monto;
    });

    document.getElementById("total").textContent = total;
}

function agregar() {
    let cliente = document.getElementById("cliente").value;
    let monto = parseFloat(document.getElementById("monto").value);
    let pago = document.getElementById("pago").value;

    if(cliente === "" || isNaN(monto) || pago === "") {
        alert("Completa todos los datos");
        return;
    }

    let fecha = new Date().toLocaleString();

    pedidos.push({cliente, monto, pago, fecha});
    guardar();
    mostrar();

    document.getElementById("cliente").value = "";
    document.getElementById("monto").value = "";
    document.getElementById("pago").value = "";
}

function eliminar(i) {
    pedidos.splice(i, 1);
    guardar();
    mostrar();
}

mostrar();
</script>

</body>
</html>
