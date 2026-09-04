<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TERMINAL OPENCHAIN</title>
    <style>
        /* Colores Estilo Cyberpunk */
        body {
            background-color: #0b020f;
            color: #d883ff;
            font-family: 'Courier New', Courier, monospace;
            margin: 0;
            padding: 15px;
            display: flex;
            justify-content: center;
        }
        /* Contenedor que simula la pantalla del teléfono */
        .phone-screen {
            width: 100%;
            max-width: 400px;
            background: #13031a;
            border: 2px solid #a32cc4;
            border-radius: 12px;
            padding: 15px;
            box-shadow: 0 0 15px rgba(163, 44, 196, 0.4);
            box-sizing: border-box;
        }
        .header {
            text-align: center;
            border-bottom: 1px double #a32cc4;
            padding-bottom: 8px;
            margin-bottom: 15px;
            font-weight: bold;
            letter-spacing: 2px;
        }
        /* Cuadrícula de Criptomonedas */
        .node-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
            margin-bottom: 15px;
        }
        .node-card {
            background: #22062b;
            border: 1px solid #70198a;
            padding: 8px;
            text-align: center;
            font-size: 11px;
            word-break: break-all;
        }
        .node-card.active {
            background: #a32cc4;
            color: #fff;
            box-shadow: 0 0 8px #a32cc4;
        }
        /* Pantalla de la Terminal */
        .terminal-box {
            background: #07010a;
            border: 1px solid #501063;
            height: 220px;
            padding: 10px;
            font-size: 11px;
            overflow-y: auto;
            line-height: 1.4;
            margin-bottom: 15px;
            color: #e6a8ff;
        }
        .ln-success { color: #00ff66; }
        .ln-warn { color: #ffcc00; }
        
        .footer-btn {
            background: #340942;
            color: #ffb3ff;
            border: 1px solid #a32cc4;
            width: 100%;
            padding: 12px;
            font-family: inherit;
            cursor: pointer;
            text-transform: uppercase;
            font-weight: bold;
        }
    </style>
</head>
<body>

<div class="phone-screen">
    <div class="header">MR. OPENCHAIN v1.0</div>
    
    <!-- Botones de las Monedas -->
    <div class="node-grid">
        <div id="btc-card" class="node-card active">■ BTC: $---</div>
        <div id="eth-card" class="node-card">■ ETH: $---</div>
        <div id="ltc-card" class="node-card">■ LTC: $---</div>
    </div>

    <!-- Consola de Texto -->
    <div class="terminal-box" id="termLog">
        > iniciando sistema local en el navegador...<br>
        > cargando módulos criptográficos... <span class="ln-success">[OK]</span><br>
        > entorno aislado y seguro listo.<br>
        <span class="ln-warn">> esperando ejecución de escaneo...</span><br>
    </div>

    <button class="footer-btn" onclick="triggerAction()">Escanear Precios Reales</button>
</div>

<script>
    // Función corregida que conecta con el mercado real
    async function triggerAction() {
        const log = document.getElementById('termLog');
        log.innerHTML += `> conectando con API de CoinGecko...<br>`;
        log.scrollTop = log.scrollHeight;

        try {
            // Petición segura a los servidores de CoinGecko
            const response = await fetch('https://coingecko.com');
            const data = await response.json();

            // Insertar los precios reales usando IDs específicos
            document.getElementById('btc-card').innerText = `■ BTC: $${data.bitcoin.usd}`;
            document.getElementById('eth-card').innerText = `■ ETH: $${data.ethereum.usd}`;
            document.getElementById('ltc-card').innerText = `■ LTC: $${data.litecoin.usd}`;

            log.innerHTML += `<span class="ln-success">> ¡Datos del mercado sincronizados con éxito!</span><br>`;
        } catch (error) {
            log.innerHTML += `<span class="ln-warn">> error de red externa. reconectando...</span><br>`;
        }
        log.scrollTop = log.scrollHeight;
    }
</script>

</body>
</html>
