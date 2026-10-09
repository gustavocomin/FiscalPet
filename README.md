# 🐾 FiscalPet

**Monitoramento inteligente de animais de estimação com inteligência artificial.**

O FiscalPet é um projeto de código aberto voltado ao monitoramento de animais de estimação em ambientes externos, utilizando câmeras IP, visão computacional e alertas em tempo real para identificar situações de possível fuga.

O objetivo é permitir que cães e gatos circulem livremente em áreas cercadas, enquanto o sistema monitora automaticamente regiões de risco e notifica seus responsáveis quando uma intervenção pode ser necessária.

## 🎯 Objetivo

Desenvolver uma solução de monitoramento automatizado capaz de:

- Detectar cães e gatos utilizando inteligência artificial.
- Monitorar zonas de risco configuráveis, como cercas, grades e portões.
- Identificar aproximações potencialmente perigosas.
- Enviar alertas pelo Telegram com imagens das detecções.
- Abrir automaticamente uma janela de monitoramento no Windows quando ocorrer um alerta.
- Reduzir falsos positivos e notificações repetidas.
- Registrar eventos para análise e ajustes futuros.

O FiscalPet funciona como uma camada adicional de segurança e não substitui barreiras físicas adequadas.

## 🏗️ Arquitetura

O projeto utiliza uma arquitetura orientada a eventos, integrando o Frigate a serviços desenvolvidos em .NET.

```text
           ┌──────────────────┐
           │    Câmeras IP    │
           │    RTSP / PoE    │
           └────────┬─────────┘
                    │
                    ▼
           ┌──────────────────┐
           │     Frigate      │
           │  Detecção por IA │
           │  Zonas de risco  │
           └────────┬─────────┘
                    │
                    ▼
           ┌──────────────────┐
           │       MQTT       │
           │ Eventos em tempo │
           │       real       │
           └────────┬─────────┘
                    │
                    ▼
           ┌──────────────────┐
           │ FiscalPet Backend│
           │      .NET        │
           │ Regras e alertas │
           └────────┬─────────┘
                    │
           ┌────────┴────────┐
           ▼                 ▼
  ┌────────────────┐ ┌────────────────┐
  │    Telegram    │ │  Agente Windows│
  │ Foto e alerta  │ │ Janela ao vivo │
  └────────────────┘ └────────────────┘
```

## 🛠️ Tecnologias

| Tecnologia | Finalidade |
|---|---|
| C# / .NET | Backend, processamento de eventos e integrações |
| Frigate NVR | Detecção de objetos por inteligência artificial |
| OpenVINO | Aceleração da inferência dos modelos de detecção |
| MQTT | Comunicação de eventos entre componentes |
| Telegram Bot API | Envio de notificações e imagens |
| WPF + WebView2 | Aplicativo Windows para monitoramento automático |
| Docker / Docker Compose | Execução e gerenciamento dos serviços |
| RTSP | Recebimento dos vídeos das câmeras IP |

## 🚨 Sistema de alertas

Quando um animal é detectado em uma zona de risco, o FiscalPet poderá executar automaticamente as seguintes ações:

**1. Notificação pelo Telegram**

Envio de uma mensagem contendo:

- Tipo de animal detectado.
- Câmera responsável pela detecção.
- Data e horário do evento.
- Imagem capturada pelo Frigate.
- Link para visualização, quando disponível.

**2. Monitoramento automático no Windows**

Um agente local abrirá uma janela dedicada à câmera responsável pelo alerta, com:

- Visualização ao vivo.
- Janela independente e configurada para permanecer em primeiro plano.
- Notificação sonora.
- Identificação do evento.
- Opção para dispensar o alerta.

**3. Controle de notificações**

O backend poderá aplicar regras de prioridade, intervalos mínimos entre alertas e tratamento de eventos repetidos.

## 📋 Funcionalidades e progresso

### Infraestrutura e detecção

- [x] Executar o Frigate utilizando Docker.
- [x] Integrar câmera IP por RTSP.
- [x] Configurar detecção de cães, gatos e pessoas.
- [x] Validar a execução do detector OpenVINO.
- [ ] Integrar múltiplas câmeras.
- [ ] Configurar zonas de risco.
- [ ] Validar detecções em situações reais.

### Backend

- [ ] Criar o backend FiscalPet em .NET.
- [ ] Integrar eventos do Frigate via MQTT.
- [ ] Implementar regras de detecção e alerta.
- [ ] Implementar controle de notificações repetidas.
- [ ] Integrar a API de snapshots do Frigate.
- [ ] Integrar o Telegram Bot API.
- [ ] Registrar histórico de eventos.

### Aplicativo Windows

- [ ] Desenvolver agente Windows com WPF.
- [ ] Integrar WebView2 para visualização das câmeras.
- [ ] Implementar abertura automática da janela.
- [ ] Implementar comportamento Always on Top.
- [ ] Adicionar notificações sonoras.
- [ ] Permitir dispensar alertas.
- [ ] Configurar inicialização automática com o Windows.

## 🔒 Privacidade e segurança

O FiscalPet foi idealizado para operar preferencialmente em infraestrutura própria, mantendo o processamento das imagens sob controle do responsável pelo sistema.

A arquitetura prioriza:

- Processamento local dos vídeos.
- Comunicação autenticada entre serviços.
- Proteção das credenciais das câmeras e integrações.
- Configuração de acesso às interfaces de monitoramento.
- Compartilhamento de imagens apenas com destinatários autorizados.

O envio de imagens pelo Telegram é opcional e depende de configuração explícita.

## 🚧 Status do projeto

**Em desenvolvimento — prova de conceito.**

A integração inicial entre uma câmera IP e o Frigate já foi validada, incluindo a execução do detector de objetos.

As integrações MQTT, backend .NET, notificações Telegram e aplicativo Windows fazem parte das próximas etapas de desenvolvimento.

## 🌎 English

### About FiscalPet

**FiscalPet is an AI-powered pet monitoring and escape alert system.**

The project aims to help pet owners monitor dogs and cats in fenced outdoor areas using IP cameras, computer vision and real-time notifications.

By combining Frigate NVR, MQTT and .NET, FiscalPet is designed to detect pets approaching configurable risk zones and automatically notify their owners.

### Planned features

- AI-powered cat and dog detection.
- Configurable monitoring and risk zones.
- Real-time event processing using MQTT.
- Telegram notifications with detection snapshots.
- Automatic live camera pop-up on Windows.
- Sound alerts and notification cooldowns.
- Support for multiple IP cameras.
- Local-first video processing.

### Tech stack

C# / .NET · Frigate NVR · OpenVINO · MQTT · Telegram Bot API · WPF · WebView2 · Docker · RTSP

### Project status

**Work in progress — proof of concept.**

Initial IP camera integration and object detection with Frigate have been validated. Backend services, Telegram notifications and the Windows monitoring agent are planned.

### Disclaimer

FiscalPet is intended as an additional monitoring and safety layer. It does not guarantee escape prevention and should not replace appropriate physical barriers or responsible supervision.

---

**FiscalPet** — Tecnologia para cuidar de quem faz parte da família. 🐾
