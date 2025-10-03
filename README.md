# Detector portátil de Metanol – ESP32 + LCD 16×2 + MQ-3 + MQ-138

Projeto experimental de **baixo custo** para **triagem** de bebidas alcoólicas, ajudando a identificar possíveis adulterações com **metanol**.

⚠️ Aviso: este dispositivo é apenas um **detector de risco**. Não substitui análise laboratorial.  
Se houver suspeita de adulteração, **não consuma**.

---

## Materiais necessários
- 1x ESP32 DevKit v1
- 1x Display LCD 16×2 com módulo I2C (PCF8574)
- 1x Sensor MQ-3 (álcool/etanol)
- 1x Sensor MQ-138 (ou TGS822)
- 2x resistores de carga (10k–47k se não vier no módulo)
- Protoboard + jumpers
- Fonte USB 5V (mínimo 1A)

---

## Ligações

### ESP32 → LCD I2C
- **VCC** → 5V  
- **GND** → GND  
- **SDA** → GPIO21  
- **SCL** → GPIO22  

### ESP32 → MQ-3
- **AOUT** → GPIO34  
- **VCC** → 5V  
- **GND** → GND  
- **H+ / H-** → 5V / GND  

### ESP32 → MQ-138
- **AOUT** → GPIO35  
- **VCC** → 5V  
- **GND** → GND  
- **H+ / H-** → 5V / GND  

---

## Uso
1. Ligue os sensores por 24–48h em ar limpo (queima inicial).
2. Calibre em **etanol conhecido** (ex.: álcool 70% ou bebida confiável).
3. Meça a bebida suspeita em frasco fechado por 1–2 min.
4. O display mostrará:
   - Leituras dos dois sensores (ADC)
   - Razão (RATIO)
   - Status: `OK` ou `ALERTA`

---

## Lógica
- O MQ-3 responde melhor a **etanol**.  
- O MQ-138 responde relativamente mais a **metanol e VOCs leves**.  
- Se a razão MQ-138/MQ-3 for **muito maior** do que no padrão calibrado → `ALERTA`.

---

## Exemplo de saída (LCD)

```
Q3:1200 Q138:2200
R:1.83 ALERTA
```

---

## Roadmap
- [ ] Versão com compensação de temperatura/umidade (BME280).
- [ ] Adicionar micro-bomba para amostragem mais estável.
- [ ] Treinamento com ML para melhorar seletividade.
