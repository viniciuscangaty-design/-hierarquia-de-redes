# Atividade 4 - Rede Hierárquica

## Descrição

Foi realizada a montagem de uma rede hierárquica utilizando o Cisco Packet Tracer, seguindo a estrutura proposta na atividade.

A rede foi dividida em três camadas:

- Core (Núcleo)
- Distribution (Distribuição)
- Edge (Borda)

## Estrutura da rede

A topologia possui:

- 1 roteador (R1);
- 2 switches de Core;
- 4 switches de Distribution;
- 4 switches de Edge;
- 4 computadores;
- 4 notebooks;
- 1 servidor.

### Camada Core

Os dois switches de Core foram interligados por 4 enlaces físicos, permitindo uma futura agregação de links de 4 Gbps.

O roteador R1 possui duas interfaces FastEthernet, sendo uma conectada ao Core-SW1 e outra ao Core-SW2.

### Camada Distribution

Foram utilizados 4 switches de Distribution.

Os switches de Core foram conectados aos switches de Distribution utilizando enlaces de fibra óptica.

Cada conexão entre Core e Distribution possui 2 enlaces, permitindo uma futura agregação de links de 2 Gbps.

### Camada Edge

Foram utilizados 4 switches de Edge.

Cada switch de Edge está conectado a um switch de Distribution e aos dispositivos finais da rede.

## Dispositivos finais

A rede possui:

- 4 computadores;
- 4 notebooks;
- 1 servidor.

Todos os dispositivos finais foram conectados por cabos de rede.

## Configuração IPv4 - Ponto Extra

Para realizar o ponto extra da atividade, foram configurados endereços IPv4 nos dispositivos finais.

### Computadores

| Dispositivo | IPv4 |
|---|---|
| PC1 | 192.168.10.10 |
| PC2 | 192.168.10.11 |
| PC3 | 192.168.10.12 |
| PC4 | 192.168.10.13 |

### Notebooks

| Dispositivo | IPv4 |
|---|---|
| Note1 | 192.168.10.20 |
| Note2 | 192.168.10.21 |
| Note3 | 192.168.10.22 |
| Note4 | 192.168.10.23 |

### Servidor

| Dispositivo | IPv4 |
|---|---|
| Servidor | 192.168.10.30 |

### Configurações utilizadas

*Rede:* 192.168.10.0/24

*Máscara de sub-rede:* 255.255.255.0

*Gateway padrão:* 192.168.10.1

## Teste de comunicação

Após a configuração dos endereços IPv4, foram realizados testes de comunicação utilizando o comando ping.

Os testes foram realizados entre os dispositivos da rede e apresentaram comunicação, confirmando a conectividade entre os equipamentos.

## Diagrama da rede

O print do diagrama da rede está disponível neste repositório.

## Arquivo do Cisco Packet Tracer

O arquivo da atividade está disponível neste repositório:

atividade4.pkt

## Conclusão

A atividade permitiu a montagem e simulação de uma rede hierárquica, utilizando as camadas Core, Distribution e Edge.

Também foi realizado o ponto extra com a configuração dos endereços IPv4 e testes de comunicação entre os dispositivos.
