# taktflow-med-monitor

Open-source vital signs monitor firmware — IEC 62304 Class B.

## Standards

- **IEC 62304:2006+AMD1** — software lifecycle (primary)
- **ISO 14971:2019** — risk management
- **ISO 13485:2016** — quality management
- **IEC 60601-1-8** — alarm systems
- **MISRA C:2012** — coding standard

## Architecture

- **VSM** (Vital Signs Monitor): STM32G474RE — sensor acquisition, alarm detection
- **SC** (Safety Controller): TMS570LC4357 — independent lockstep supervision
- **GW** (Gateway): Raspberry Pi 4 — dashboard, MQTT, cloud bridge
- Communication: CAN bus @ 500 kbps

## Sensors

- MAX30102 (I2C) — SpO2 + heart rate
- ADS1292R (SPI) — ECG 2-channel
- MLX90614 (I2C) — body temperature

## Rules

- Follow IEC 62304 clause structure for documentation
- MISRA C:2012 compliance required — zero violations
- All safety-critical code requires unit tests
- Risk controls must trace back to ISO 14971 risk analysis
- Never modify upstream vendor HAL code
- Platform abstraction: all MCU access through MCAL layer
