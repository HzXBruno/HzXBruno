<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Pedido de Namoro</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background: #1a1a1a;
            color: #fff;
            margin: 0;
            padding: 0;
            overflow: hidden;
        }
        
        h1 {
            color: #ff0080;
            margin-top: 100px;
            font-size: 36px;
        }
        
        .pedido {
            margin-bottom: 50px;
        }
        
        .botoes {
            display: flex;
            justify-content: center;
            margin-top: 50px;
        }
        
        .botao {
            display: inline-block;
            padding: 10px 20px;
            font-size: 20px;
            background-color: #ff0080;
            color: #fff;
            border: none;
            cursor: pointer;
            margin: 0 10px;
            transition: transform 0.3s;
            border-radius: 5px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
            position: absolute;
        }
        
        .botao:hover {
            transform: scale(1.1);
        }
        
        .animacao {
            display: none;
            margin-top: 50px;
            font-size: 24px;
            color: #ff0080;
            animation-name: pulsar;
            animation-duration: 2s;
            animation-iteration-count: infinite;
        }
        
        @keyframes pulsar {
            0% {
                transform: scale(1);
            }
            50% {
                transform: scale(1.2);
            }
            100% {
                transform: scale(1);
            }
        }
    </style>
    <script src="https://hammerjs.github.io/dist/hammer.min.js"></script>
    <script>
        window.addEventListener('load', function() {
            var simButton = document.getElementById('sim');
            var naoButton = document.getElementById('nao');
            var animacaoDiv = document.getElementById('animacao');
            var isTouchDevice = false;
            
            // Verifica se o dispositivo é um dispositivo de toque (celular ou tablet)
            if ('ontouchstart' in window || navigator.maxTouchPoints) {
                isTouchDevice = true;
            }
            
            simButton.addEventListener('click', function() {
                simButton.style.display = 'none';
                naoButton.style.display = 'none';
                animacaoDiv.style.display = 'block';
                animacaoDiv.classList.add('animacao');
            });
            
            if (!isTouchDevice) {
                var maxX = window.innerWidth - naoButton.offsetWidth;
                var maxY = window.innerHeight - naoButton.offsetHeight;
                
                document.addEventListener('mousemove', function(e) {
                    var mouseX = e.clientX;
                    var mouseY = e.clientY;
                    
                    var naoButtonRect = naoButton.getBoundingClientRect();
                    var naoButtonX = naoButtonRect.left + naoButtonRect.width / 2;
                    var naoButtonY = naoButtonRect.top + naoButtonRect.height / 2;
                    
                    var distance = Math.sqrt(Math.pow(mouseX - naoButtonX, 2) + Math.pow(mouseY - naoButtonY, 2));
                    
                    if (distance < 100) {
                        var newX = Math.floor(Math.random() * (maxX - naoButton.offsetWidth));
                        var newY = Math.floor(Math.random() * (maxY - naoButton.offsetHeight));
                        
                        naoButton.style.left = newX + 'px';
                        naoButton.style.top = newY + 'px';
                    }
                });
            } else {
                var mc = new Hammer(naoButton);
                var startX, startY;
                var buttonRect = naoButton.getBoundingClientRect();
                
                mc.on("panstart", function(e) {
                    startX = buttonRect.left;
                    startY = buttonRect.top;
                });
                
                mc.on("panmove", function(e) {
                    var newX = startX + e.deltaX;
                    var newY = startY + e.deltaY;
                    
                    naoButton.style.left = newX + 'px';
                    naoButton.style.top = newY + 'px';
                });
            }
        });
    </script>
</head>

<body>
    <div class="pedido">
        <h1>Quer namorar comigo?</h1>
    </div>
    <div class="botoes">
        <button id="sim" class="botao">Sim</button>
        <button id="nao" class="botao">Não</button>
    </div>
    <div id="animacao" class="animacao">
        Parabéns! Você aceitou o pedido de namoro. 🎉
    </div>
</body>

</html>
