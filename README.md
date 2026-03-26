# taktflow-med-monitor

Open-source patient vital signs monitor — IEC 62304 Class B medical device firmware.

## Purpose

Embedded firmware for a multi-parameter vital signs monitor targeting early
detection of physiological anomalies. Built on STM32 + TMS570 safety
architecture with CAN-based data transport.

## Target Standards

| Standard | Scope |
|----------|-------|
| IEC 62304:2006+AMD1 | Software lifecycle for medical devices |
| ISO 14971:2019 | Risk management |
| ISO 13485:2016 | Quality management system |
| IEC 60601-1-8 | Alarm systems in medical equipment |
| MISRA C:2012 | Coding standard |

## Software Safety Classification

**IEC 62304 Class B** — software that could contribute to a hazardous
situation but is not the sole risk control.

## Hardware Platform

| Board | MCU | Role |
|-------|-----|------|
| NUCLEO-G474RE | STM32G474RE (Cortex-M4F) | Vital Signs Monitor (VSM) — sensor acquisition |
| LAUNCHXL2-570LC43 | TMS570LC4357 (lockstep) | Safety Controller (SC) — independent supervision |
| Raspberry Pi 4 | BCM2711 | Gateway — dashboard, MQTT, cloud bridge |

## Sensors

| Sensor | Interface | Measurement |
|--------|-----------|-------------|
| MAX30102 | I2C | SpO2 + heart rate (PPG) |
| ADS1292R | SPI | ECG (2-channel, 24-bit) |
| MLX90614 | I2C | Non-contact body temperature |

## Architecture

```
STM32G474 (VSM ECU)
  +-- MAX30102 (SpO2/HR)    [I2C1]
  +-- ADS1292R (ECG)        [SPI1]
  +-- MLX90614 (Temp)       [I2C1]
  +-- CAN bus (500 kbps)
        |
        +-- TMS570 (SC) -- watchdog supervision, alarm relay
        +-- Pi Gateway  -- dashboard, MQTT, alarm engine
```

## Build

```bash
# POSIX SIL (desktop simulation)
make -f Makefile.posix

# STM32 target
make -f Makefile.stm32

# Unit tests
make -f Makefile.test

# MISRA check
make -f Makefile.misra
```

## Project Structure

See `docs/INDEX.md` for full documentation map.

## License

BSD-3-Clause
