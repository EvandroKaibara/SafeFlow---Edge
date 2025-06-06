
# Monitoramento de Nível com Sensor Ultrassônico e MQTT

## 📌 Descrição do Problema

O monitoramento de nível de líquidos, como em reservatórios de água, é essencial para garantir o funcionamento adequado de sistemas hidráulicos e evitar desperdícios ou falhas críticas. Uma medição imprecisa ou a falta de alertas visuais pode comprometer toda a operação.

## 💡 Solução Proposta

Este projeto utiliza um sensor ultrassônico HC-SR04 conectado a um ESP32 para medir a distância (nível do líquido). O sistema envia os dados em tempo real via protocolo MQTT para um broker público (`broker.hivemq.com`). Além disso, três LEDs indicam visualmente o estado do nível:
- **Verde**: Nível seguro (> 300 cm)
- **Amarelo**: Atenção (entre 100 cm e 300 cm)
- **Vermelho**: Crítico (< 100 cm)

Os dados são publicados em formato JSON no tópico `agua/monitoramento`, podendo ser integrados a um dashboard Node-RED para visualização remota.

## ▶️ Instruções de Execução e Simulação

### Requisitos
- Conta no [Wokwi](https://wokwi.com)
- Navegador com acesso à internet

### Passos
1. Acesse o link do projeto no Wokwi (ver abaixo).
2. Aguarde a conexão com o Wi-Fi virtual (SSID: `Wokwi-GUEST`, canal 6).
3. Observe a medição da distância e o acendimento dos LEDs conforme a simulação.
4. Os dados em JSON são publicados no broker MQTT.
5. No Node-RED, conecte-se ao mesmo tópico MQTT (`agua/monitoramento`) para receber os dados e montar o dashboard.

## 🌐 Link importantes

👉 [Acessar simulação Wokwi](https://wokwi.com/projects/432973590739623937) 
👉 [Acessar vídeo explicativo](https://www.youtube.com/watch?v=mPsRiQh9ca8) 

## 📦 Formato da Publicação MQTT

```json
{
  "distancia": 97,
  "status": "Crítico",
  "led": "vermelho"
}
```

---
## Desenvolvedores

- Evandro Yuji Kaibara de Oliveira RM: 559274
- Mateus da Rocha Mallet RM: 560491


Editor: Wokwi  
Linguagem: C++ (Arduino ESP32)
