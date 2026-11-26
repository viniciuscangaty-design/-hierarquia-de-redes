# Atividade Prática 07 – Ambiente Hierárquico com VLANs e Trunk (802.1Q)

Simulação no **Cisco Packet Tracer** de uma rede hierárquica (Núcleo, Distribuição e Acesso) com enlaces **trunk** entre os switches, permitindo o tráfego das VLANs 10 e 20.

## 1. Objetivo

Configurar o modo trunk nas portas de interligação das camadas de **Acesso**, **Distribuição** e **Núcleo**, garantindo que as VLANs 10 (Alunos) e 20 (Visitantes) trafeguem por esses enlaces.

## 2. Topologia

![Topologia](docs/topologia.png)

| Camada | Dispositivos |
|---|---|
| Roteador | R1 (Cisco 1841) |
| Núcleo | CORE1 (`SW_CORE_01`), CORE2 (`SW_CORE_2`) |
| Distribuição | DIST1 (`SW_DIST_1`), DIST2 (`SW_DIST_2`) |
| Acesso | ACC_1, ACC_2 (ligados à DIST1); ACC3, ACC_4 (ligados à DIST2) – Cisco 2960-24TT |
| Estações | PC1–PC4 e note1–note4 (um PC e um notebook por switch de acesso), Servidor |

## 3. Fundamentação: IEEE 802.1Q

- **Porta trunk:** porta que transporta o tráfego de várias VLANs em um único enlace físico entre switches.
- **Encapsulamento 802.1Q:** o switch insere no quadro Ethernet uma tag de 4 bytes que carrega o ID da VLAN (12 bits, valores 1 a 4094). Assim, o switch do outro lado sabe a qual VLAN o quadro pertence.
- **VLAN nativa (native VLAN):** é a VLAN cujo tráfego trafega **sem tag** no trunk. Por padrão é a VLAN 1, e deve ser a mesma nas duas pontas do enlace.
- **Lista de VLANs permitidas (allowed VLANs):** por padrão o trunk permite todas as VLANs (1–1005). Neste trabalho foi restringida para **10 e 20**, o que reduz tráfego desnecessário.

## 4. VLANs

| ID | Nome | Uso |
|---|---|---|
| 10 | Alunos | Estações de alunos |
| 20 | Visitantes | Estações de visitantes |
| 1 | default | VLAN nativa dos trunks |

## 5. Interfaces trunk por switch

Resultado de `show interfaces trunk` em cada equipamento (modo `on` = trunk forçado; todos com encapsulamento 802.1q e VLAN nativa 1).

### Acesso

| Switch | Interface | Modo | VLANs permitidas | Conecta a |
|---|---|---|---|---|
| ACC_1 | Gig0/1 | trunk | 10,20 | DIST1 |
| ACC_2 | Gig0/1 | trunk | 10,20 | DIST1 |
| ACC3 | Gig0/1 | trunk | 10,20 | DIST2 |
| ACC_4 | Gig0/1 | trunk | 10,20 | DIST2 |

### Distribuição

| Switch | Interface | Modo | VLANs permitidas | Conecta a |
|---|---|---|---|---|
| DIST1 | Gig0/1 | trunk | 10,20 | CONFIRMAR |
| DIST1 | Gig1/1 | trunk | 10,20 | CONFIRMAR |
| DIST1 | Gig6/1 | trunk | 10,20 | CONFIRMAR |
| DIST1 | Gig9/1 | trunk | 10,20 | CONFIRMAR |
| DIST2 | Gig0/1 | trunk | 10,20 | CONFIRMAR |
| DIST2 | Gig1/1 | trunk | 10,20 | CONFIRMAR |
| DIST2 | Gig5/1 | trunk | 10,20 | CONFIRMAR |
| DIST2 | Gig6/1 | trunk | 10,20 | CONFIRMAR |

### Núcleo

| Switch | Interface | Modo | VLANs permitidas | Conecta a |
|---|---|---|---|---|
| CORE1 | Gig3/1 | trunk | 10,20 | CONFIRMAR |
| CORE1 | Gig4/1 | trunk | 10,20 | CONFIRMAR |
| CORE1 | Gig6/1 | trunk | 10,20 | CONFIRMAR |
| CORE1 | Gig7/1 | trunk | 10,20 | CONFIRMAR |
| CORE1 | Gig8/1 | trunk | 10,20 | CONFIRMAR |
| CORE2 | Gig4/1 | trunk | 10,20 | CONFIRMAR |
| CORE2 | Gig5/1 | trunk | 10,20 | CONFIRMAR |
| CORE2 | Gig7/1 | trunk | 10,20 | CONFIRMAR |
| CORE2 | Gig8/1 | trunk | 10,20 | CONFIRMAR |
| CORE2 | Gig9/1 | trunk | 10,20 | CONFIRMAR |

> **Nota sobre o STP:** em alguns enlaces redundantes a saída mostra `none` em "forwarding state and not pruned" (por exemplo CORE1 Gig4/1 e DIST2 Gig0/1). Isso é o Spanning Tree bloqueando um dos caminhos para evitar loops; o trunk continua configurado corretamente.

## 6. Comandos de configuração

Os comandos completos, por switch, estão em [`comandos.txt`](comandos.txt). Modelo para um switch de acesso:

```
enable
configure terminal
interface GigabitEthernet0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20
end
write memory
```

Para várias portas de uma vez (distribuição e núcleo), use `interface range`:

```
interface range GigabitEthernet0/1 , GigabitEthernet1/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20
```

## 7. Verificação

```
show interfaces trunk
show vlan brief
```

Prints da verificação em cada switch estão na pasta [`docs/`](docs/).

## 8. Arquivos do repositório

| Arquivo | Conteúdo |
|---|---|
| `README.md` | Este tutorial |
| `comandos.txt` | Comandos do Cisco IOS por switch |
| `docs/topologia.png` | Diagrama atualizado |
| `docs/` | Prints do `show interfaces trunk` de cada switch |
