# SafeFlow

Este projeto tem o objeto de medir a distância da água até o limite para que comece uma enchente.

## Componentes Utilizados

- ESP32 Devkit
- Sensor Ultrassônico HC-SR04
- LEDs (Verde, Amarelo, Vermelho)
- Resistores
- Plataforma Wokwi para simulação
- Broker MQTT (broker.hivemq.com)
- Node-RED

## Lógica de Funcionamento

1. O sensor ultrassônico mede a distância.
2. De acordo com a distância, um LED acende:
   - **Verde**: > 300 cm → "Tudo certo"
   - **Amarelo**: entre 100 cm e 300 cm → "Ficar atento"
   - **Vermelho**: < 100 cm → "Crítico"
3. Os dados são enviados em formato JSON via MQTT:
```json
{
  "distancia": 97,
  "status": "Crítico",
  "led": "vermelho"
}
```

## Configuração do Wi-Fi no Wokwi

Certifique-se de usar o seguinte trecho no `setup_wifi()`:
```cpp
WiFi.begin("Wokwi-GUEST", "", 6);  // Canal 6 obrigatório
```

## Dashboard Node-RED

### Fluxo
- MQTT IN (topico: `agua/monitoramento`)
- JSON
- Function: separa distância e status
- ui_text: exibe distância
- ui_text: exibe status com cores (vermelho/lime/laranja)

### Function para distância
```js
msg.payload = "Distância: " + msg.payload.distancia + " cm";
return msg;
```

### Function para status
```js
let status = msg.payload.status;
msg.payload = "Status do LED: " + status;

if (status === "Crítico") {
    msg.color = "#ff0000";
    msg.bold = true;
} else if (status === "Ficar atento") {
    msg.color = "#ff9900";
    msg.bold = true;
} else {
    msg.color = "#00cc00";
    msg.bold = true;
}
return msg;
```

## Autor

Evandro Yuji Kaibara de Olveira RM: 559274
Mateus da Rocha Mallet RM: 560491