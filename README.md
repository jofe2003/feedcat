# FeedCat 🐱

> **Versão v1 (semana 1): protótipo de recepção serial.** Para ver a versão final, use a tag [`v3`](../../tree/v3).

Alimentador inteligente que só libera a comida para o gato certo, identificado pelo **peso**.

Projeto final da disciplina **PCS3645 – Laboratório Digital II** (Escola Politécnica da USP, 2024).

## O que esta versão faz

Primeiro passo da comunicação ESP32 → FPGA. O circuito `hardware/Verilog/circuito.v`:

1. recebe bytes pela UART (`rx_serial_8n1_nandland`, 115200 baud, 8N1, com clock de 50 MHz);
2. guarda o último byte recebido em um registrador;
3. converte o caractere ASCII (`'0'`–`'9'`) para binário e mostra o valor num display de 7 segmentos.

Os demais módulos (`servo/`, `contador_cm/`, `modulos/`) vieram das experiências anteriores da disciplina e foram usados nas semanas seguintes.

## Simulação

```bash
cd hardware/Verilog
python comp.py               # gera comp.txt com os .v que não são testbench
echo circuito_tb.v >> comp.txt
iverilog -o circuito.out -c comp.txt
vvp circuito.out
gtkwave wave.vcd ../Misc/circuito_tb.gtkw
```

O projeto do Quartus está em `hardware/Quartus/circuito.qar`. Para abrir, use **Project → Restore Archived Project**.

## Conteúdo

| Pasta | Descrição |
|---|---|
| `docs/` | Especificação, arquitetura e pseudocódigo (da v0) |
| `hardware/Verilog/` | Código Verilog e testbench |
| `hardware/Quartus/` | Projeto arquivado do Quartus |
| `hardware/Misc/` | Layout do GTKWave |

## Equipe

- Felipe Luis Korbes
- João Felipe de Souza Melo
- João Felipe Pereira Carvalho
