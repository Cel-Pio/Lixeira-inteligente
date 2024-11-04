# Lixeira-inteligente
Objetivo:

O objetivo deste projeto é uma lixeira inteligente utilizando a plataforma Arduino, que facilita o descarte de resíduos de forma prática e higiênica. A lixeira é equipada com sensores que detectam a proximidade do usuário, levanta a tampa automaticamente. O projeto foi realizado com 01 Arduino,  01 Sensor de nível ultrassônico, 01 Sensor de presença, 02 atuadores: servo motor ; LED com 2 pontas e o módulo Bluetooth.
Esquema de Conexões
•	Sensor Ultrassônico (HC-SR04):
•	Trigger (Pino 7): Conecte ao pino digital 7 do Arduino.
•	Echo (Pino 6): Conecte ao pino digital 6 do Arduino.
•	VCC: Conecte à alimentação de 5V do Arduino.
•	GND: Conecte ao GND do Arduino.
•	Sensor PIR:
•	Pino de Sinal (Pino 13): Conecte ao pino digital 13 do Arduino.
•	VCC: Conecte à alimentação de 5V do Arduino.
•	GND: Conecte ao GND do Arduino.
•	LED:
•	Anodo (Pino 3): Conecte ao pino digital 3 do Arduino (use um resistor de 220 ohms em série).
•	Catodo: Conecte ao GND do Arduino.
•	Servomotor:
•	Pino de Controle (Pino 9): Conecte ao pino digital 9 do Arduino.
•	VCC: Conecte à alimentação de 5V do Arduino.
•	GND: Conecte ao GND do Arduino.
•	Módulo Bluetooth (HC-05 ou similar):
•	RX (Pino 10): Conecte ao pino digital 10 do Arduino.
•	TX (Pino 11): Conecte ao pino digital 11 do Arduino.
•	VCC: Conecte à alimentação de 5V do Arduino.
•	GND: Conecte ao GND do Arduino.
Lógica do Código
•	Configuração Inicial (setup):
•	pinMode(ultrassonicoTrigger, OUTPUT); e pinMode(sensorEcho, INPUT); configuram os pinos do sensor ultrassônico.
•	pinMode(sensorPir, INPUT); configura o pino do sensor PIR.
•	pinMode(LED, OUTPUT); configura o pino do LED.
•	Serial.begin(9600); e bt.begin(9600); inicializam a comunicação serial e Bluetooth.
•	Leitura da Distância (loop):
•	O código envia um pulso para o pino de Trigger do sensor ultrassônico (digitalWrite(ultrassonicoTrigger, HIGH);), e calcula a distância com base no tempo de retorno do pulso (distanciaMedida = (tempoRetorno / 2) * 0.0343;).
•	Verificação do Estado da Lixeira:
•	O sensor PIR verifica se a lixeira está cheia. Se o estado do PIR for HIGH, a lixeira é considerada cheia (lixeiraCheia = true;), o LED acende e o tempo em que o LED foi aceso é registrado.
•	Se o PIR retorna a LOW e a lixeira estava cheia, o estado é atualizado para não cheia.
•	Controle do LED:
•	O LED permanece aceso enquanto a lixeira estiver cheia. Após 5 segundos (ledAcesa), se a lixeira ainda estiver cheia, o LED é apagado.
•	Comunicação Bluetooth:
•	O sistema cria uma string com a distância medida e o estado da lixeira, que é enviada via Bluetooth e impressa no monitor serial.
•	Recepção de Comandos:
•	Se um comando for recebido via Bluetooth (if (bt.available())), e for o comando '1', a tampa da lixeira é aberta (servoMotor.write(180);) e permanece aberta por 5 segundos. O estado da tampa é atualizado.
•	Abertura Automática da Tampa:
•	Se a distância medida for menor que 20 cm, a tampa também é aberta automaticamente, se não estiver já aberta. Após 5 segundos, a tampa é fechada.
Resumo
Este código permite que um sistema automatizado de lixeira seja controlado por sensores e comandos Bluetooth, oferecendo uma solução prática para gerenciar o lixo de forma inteligente. O uso de sensores ultrassônicos e PIR, além do controle de um servomotor para a tampa, proporciona uma interação eficiente entre o usuário e o dispositivo.




