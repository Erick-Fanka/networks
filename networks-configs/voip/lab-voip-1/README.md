# 📞 Laboratório de Telefonia IP (VoIP) — Cisco CME no Packet Tracer

Projeto de laboratório implementando uma infraestrutura básica de **Telefonia IP (VoIP)** utilizando o Call Manager Express (CME) em um roteador Cisco no simulador Packet Tracer.

> ⚠️ **Ambiente de laboratório para fins educacionais.** As configurações de rede e telefonia refletem um cenário simulado simplificado e podem não cobrir todas as práticas de segurança de um ambiente de produção real.

---

## 🏗️ Topologia & Infraestrutura

```text
                        Roteador 2911 (CME, DHCP, Gateway)
                       /
                      / (Trunk 802.1Q)
                     /
               Switch 2960
               /         \
              /           \
             /             \
      VLAN 10 (Dados)     VLAN 150 (Voz)
       192.168.10.0/24    192.168.150.0/24
      /          \         /          \
     /            \       /            \
  PC-0            PC-1 IP Phone 1    IP Phone 2
```

### Endereçamento IP e VLANs

| Componente | VLAN | Sub-rede | IP do Gateway | Função |
|---|---|---|---|---|
| `Dados` | 10 | 192.168.10.0/24 | 192.168.10.1 | Tráfego de computadores (PCs) |
| `Voz` | 150 | 192.168.150.0/24 | 192.168.150.1 | Tráfego de telefonia (IP Phones) |
| `CME/TFTP` | 150 | - | 192.168.150.1 | Servidor TFTP para registro (Option 150) |

### Equipamentos Simulados

| Componente | Especificação |
|---|---|
| Roteador | Cisco 2911 |
| Switch | Cisco 2960-24TT |
| Telefones IP | Cisco IP Phone 7960 |
| Hosts de Dados | PCs Genéricos |

---

## 🧰 Stack Utilizada

| Tecnologia / Protocolo | Função |
|---|---|
| Cisco IOS (uck9) | Sistema operacional do roteador com licença de Unified Communications |
| CME (Telephony Service) | Call Manager Express para gerenciamento de ramais e registros |
| 802.1Q | Encapsulamento para roteamento Inter-VLAN (Router-on-a-Stick) |
| DHCP (Option 150) | Distribuição de IP e apontamento do servidor TFTP para os telefones |
| SCCP | Protocolo proprietário Cisco (Skinny) usado para comunicação dos telefones |

---

## ⚙️ Como Funciona

- **CME (Call Manager Express):** Roda nativamente no roteador Cisco através do módulo `telephony-service`, sendo responsável por atribuir números de diretório (DNs) e gerenciar os telefones registrados (`ephones`).
- **VLANs:** O Switch separa fisicamente e logicamente o tráfego de dados e voz, priorizando o tráfego de áudio na rede.
- **Router-on-a-Stick:** O Roteador roteia o tráfego entre a VLAN de dados e a VLAN de voz através de subinterfaces.
- **DHCP Option 150:** Durante a inicialização, o telefone IP recebe um endereço IP e usa a opção 150 para descobrir onde baixar suas configurações (no caso, o próprio IP do roteador).

---

## 📁 Estrutura do Repositório

```bash
lab-voip-cisco/
├── README.md                      # Documentação do laboratório
├── scripts/
│   ├── roteador.cfg               # Script de configuração do Roteador (CME, DHCP, Inter-VLAN)
│   └── switch.cfg                 # Script de configuração do Switch (Trunk, Voice VLAN)
├── midias/
│   ├── diagrama.png               # Captura da topologia no Packet Tracer
│   └── phones.png                 # Captura do teste de chamada entre os IP Phones
└── pkt/
    └── atividade-voip.pkt         # Arquivo do simulador (Cisco Packet Tracer)
```

---

## 🚀 Teste de Funcionamento

Com a rede configurada e os telefones registrados:

1.  Abra a interface gráfica (GUI) de um dos IP Phones no Packet Tracer.
2.  Verifique se o display exibe o ramal atribuído (ex: 5540).
3.  Abra a interface de outro IP Phone e disquio o número do primeiro.
4.  O telefone de destino deve tocar, e ao atender, o display exibirá `Connected`.

---

## 📌 Exemplos de Próximos Passos

- [ ] Configurar correio de voz (Voicemail).
- [ ] Conectar o ambiente a uma rede externa usando um entroncamento SIP ou FXO.

---

## 👨‍💻 Autor

**Erick da Cruz Fanka**  
Competidor WorldSkills | Estudante na Faculdade de Tecnologia SENAI Porto Alegre | Serviços de Redes | Cloud Computing | AWS | Linux