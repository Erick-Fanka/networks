---

## 🏗️ Topologia da Rede

```text
  [PC 1, 2, 3]                                [PC 4, 5, 6]
 VLAN 10, 20, 30                             VLAN 10, 20, 30
       |                                           |
       | (Acesso)                                  | (Acesso)
       |                                           |
    [SW1]                                       [SW2]
       \                                         /
        \ (Trunk - Fa0/24)      (Trunk - Fa0/23)/
         \                                     /
          +-------------- [SW3] ---------------+
                            |
                            | (Trunk - Gig0/1)
                            |
                       [Roteador] (Gig0/0)
                   (Router-on-a-Stick)
```

### Estrutura Lógica

| VLAN | Portas de Acesso (SW1 e SW2) | IP Gateway (Sub-interface do Roteador) | Encapsulamento Trunk |
|---|---|---|---|
| **10** | FastEthernet 0/1 | 192.168.10.1/24 | 802.1Q |
| **20** | FastEthernet 0/2 | 192.168.20.1/24 | 802.1Q |
| **30** | FastEthernet 0/3 | 192.168.30.1/24 | 802.1Q |

---

## 🧰 Conceitos Aplicados

- **VLANs (Virtual LANs):** Segmentação lógica da rede em domínios de broadcast isolados.
- **Trunking (802.1Q):** Permite a passagem de tráfego de múltiplas VLANs por um único link físico, adicionando "tags" aos quadros Ethernet.
- **Router-on-a-Stick:** Técnica onde um roteador usa uma única interface física dividida em múltiplas subinterfaces lógicas (uma para cada VLAN) para realizar o roteamento Inter-VLAN.

---

## 📁 Estrutura de Arquivos de Configuração

Os scripts completos e prontos para serem aplicados nos equipamentos estão localizados na raiz deste diretório. 

| Arquivo | Descrição |
|---|---|
| `router.r1.cfg` | Configuração do Roteador (Ativação física e criação das sub-interfaces lógicas para cada VLAN). |
| `switch-sw1.cfg` | Configuração do Switch de Acesso 1 (VLANs, portas de acesso para PCs e porta Trunk para SW3). |
| `switch-sw2.cfg` | Configuração do Switch de Acesso 2 (VLANs, portas de acesso para PCs e porta Trunk para SW3). |
| `switch-sw3.cfg` | Configuração do Switch de Distribuição (VLANs e portas Trunk recebendo de SW1/SW2 e enviando ao Roteador). |

> **Nota:** Para aplicar, basta copiar o conteúdo do arquivo respectivo e colar no terminal do equipamento em modo privilegiado (`enable`). Todos os scripts finalizam com `copy running-config startup-config` para salvar as alterações.

---

## 👨‍💻 Autor

**Erick da Cruz Fanka**  
Competidor WorldSkills | Estudante na Faculdade de Tecnologia SENAI Porto Alegre | Serviços de Redes | Cloud Computing | AWS | Linux
