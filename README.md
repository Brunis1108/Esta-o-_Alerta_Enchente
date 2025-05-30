# 🌊 Estação de Alerta de Enchente com Simulação por Joystick

Este projeto simula uma estação de alerta para enchentes e chuva intensa usando a placa **BitDogLab (RP2040)** e o sistema operacional de tempo real **FreeRTOS**. A entrada é feita por um joystick que simula os níveis de água e chuva, e os alertas são exibidos via display OLED, matriz de LEDs e buzzer.

## 📦 Componentes Utilizados

- **RP2040 (BitDogLab)**
- **Display OLED SSD1306** via I2C
- **Joystick** (leitura via ADC)
- **LEDs** individuais (vermelho e verde)
- **Matriz de LEDs WS2812 (5x5)**
- **Buzzer**
- **Botão para modo BOOTSEL**

## ⚙️ Funcionalidades

- **Simulação de níveis de água e chuva** com joystick (eixos X e Y)
- **Exibição no display OLED** dos níveis e status (`Normal` ou `ALERTA`)
- **Divisor vertical no display** para separar informações de água e chuva
- **Alertas visuais** com LED RGB e matriz de LEDs colorida:
  - Vermelho: Alerta de água alta
  - Laranja: Alerta de chuva intensa
- **Alertas sonoros** com buzzer:
  - Tom grave para água alta
  - Tom agudo para chuva intensa
- **Sistema multitarefa com FreeRTOS** (4 tarefas: joystick, display, LEDs e buzzer)
- **Filas FreeRTOS** para comunicação entre tarefas
- **Modo BOOTSEL** via interrupção de botão

## 🧠 Lógica de Alerta

| Condição               | Alerta        | LED         | Buzzer     |
|------------------------|---------------|-------------|------------|
| Água ≥ 70%             | `ALERTA`      | Vermelho    | Grave (200 Hz) |
| Chuva ≥ 80%            | `ALERTA`      | Laranja     | Agudo (400 Hz) |
| Caso contrário         | `Normal`      | Apagado     | Silencioso |

## 🧵 Organização das Tarefas

| Tarefa         | Responsabilidade                              |
|----------------|-----------------------------------------------|
| `vJoystickTask`| Lê joystick, envia dados para as filas        |
| `vDisplayTask` | Atualiza display OLED com níveis e status     |
| `vLedsTask`    | Controla LEDs e matriz de acordo com os alertas |
| `vBuzzerTask`  | Toca sons com base nos níveis de alerta       |

## 📷 Interface Visual

- Parte esquerda: Nível da água
- Parte direita: Volume de chuva
- Status: `Normal` ou `ALERTA`

## 🚀 Como Usar

1. Conecte a placa BitDogLab.
2. Compile e carregue o código no RP2040.
3. Movimente o joystick para simular níveis.
4. Observe os alertas nos LEDs, display e buzzer.

