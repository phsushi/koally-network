# KoAlly — Arquitetura de Rede

Documentação técnica da infraestrutura de rede do projeto **KoAlly** (missão espacial fictícia — Global Solution). O código da aplicação Java está em um repositório separado, em grupo: [Java_KoAlly_GS](https://github.com/GsMyKoally/Java_KoAlly_GS).

Este repositório reúne a parte que desenvolvi individualmente: **arquitetura de rede** (Cisco Packet Tracer) 

---

## 🌐 Arquitetura de rede

Rede segmentada em **três sub-redes IPv4**, interligadas por um roteador Cisco 1941, implementada e simulada no **Cisco Packet Tracer**.

```
                         ┌─────────────────┐
                         │  Cisco 1941     │
                         │    Router       │
                         └───────┬─────────┘
                  ┌──────────────┼──────────────┐
                  │              │              │
               Rede 1         Rede 2         Rede 3
             192.168.10.0   192.168.20.0   192.168.30.0
                  │              │              │
              SW-HABITAT     SW-KOALLY        SW-OPS
```

| Rede | Setor | Endereço | Gateway |
|---|---|---|---|
| Rede 1 | Habitat Humano (astronautas) | `192.168.10.0/24` | `192.168.10.1` (GigabitEthernet0/0) |
| Rede 2 | Central KoAlly AI (servidores/admin) | `192.168.20.0/24` | `192.168.20.1` (GigabitEthernet0/1) |
| Rede 3 | Centro de Operações | `192.168.30.0/24` | `192.168.30.1` (Vlan1, via módulo HWIC-4ESW) |

Não foi usado protocolo de roteamento dinâmico — as três redes são diretamente conectadas ao roteador. A Rede 3 usa uma interface VLAN (SVI) como gateway porque as portas do módulo HWIC-4ESW funcionam como portas de switch.

**Por que `/24` em todas as redes?** Uma `/24` oferece 254 endereços utilizáveis — muito mais do que o necessário para este projeto. A escolha não foi por economia de endereços, e sim por simplicidade de configuração, compreensão e documentação (objetivo didático).

### Protocolos e tecnologias

- **IPv4** — endereçamento e comunicação entre as três sub-redes
- **Ethernet** — conexões cabeadas (cabos Copper Straight-Through)
- **ICMP** — testes de conectividade via `ping` (ex.: `ping 192.168.20.1`)
- **ARP** — resolução de MAC dentro de cada rede local (implícito no funcionamento IP/Ethernet)
- **HTTP** — servidor hospedando a página web do projeto
- **DNS** — domínio `www.koallymars.space` resolvendo para `192.168.20.10`
- **Wi-Fi / IEEE 802.11** — Access Points conectando notebooks das Redes 1 e 3

### O que foi efetivamente implementado

- Cisco 1941 + módulo HWIC-4ESW, 3 switches, 2 Access Points, computadores, notebooks, servidores
- As três sub-redes configuradas com seus respectivos gateways
- Roteamento entre as três redes
- Servidor HTTP + servidor DNS com domínio próprio
- Testes de conectividade (`ping`) confirmando comunicação entre as três redes
- Página web (HTML/CSS) apresentando a solução, problema, tecnologia, as três redes, benefícios e ODS

### O que ficou apenas como arquitetura conceitual (não implementado na rede)

O Packet Tracer simula a **infraestrutura de comunicação**, não a aplicação de IA em si. Ficam fora do escopo de rede: agente de IA embarcado, monitoramento de saúde mental/biométrico, score psicológico, acionamento automático de psicólogo, scheduler adaptativo de tarefas, e comunicação real via satélite. A Rede 3 representa o Centro de Operações, mas não está conectada a sensores físicos reais.

---

## 📄 Documentos

- `docs/KoAlly_Redes.pdf` — documentação completa de rede
- `docs/koAlly_Agile_Final.pdf` — documentação do processo ágil do projeto

---

## 🔗 Projeto relacionado

Aplicação Java (grupo): [Java_KoAlly_GS](https://github.com/GsMyKoally/Java_KoAlly_GS)
