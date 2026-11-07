# ATIVIDADE PRÁTICA 06 – CONFIGURAÇÃO DE VLANs ACCESS

## 1. Objetivo

Configurar duas VLANs nos switches da camada de acesso de uma rede hierárquica,
realizando a separação lógica dos dispositivos conectados.

Foram utilizadas duas VLANs:

| ID | Nome | Finalidade |
|---|---|---|
| 10 | ALUNOS | Computadores |
| 20 | VISITANTES | Notebooks |

## 2. Topologia da rede

A atividade utiliza uma arquitetura hierárquica composta pelas camadas de núcleo (Core),
distribuição (Distribution) e acesso (Access).

A configuração desta atividade foi aplicada nos seguintes switches:

- SW_ACC_1
- SW_ACC_2
- SW_ACC_3
- SW_ACC_4

## 3. Mapeamento das interfaces

Foi estabelecido o seguinte padrão de distribuição:

**VLAN 10 – ALUNOS**

Portas ímpares:
- Fa0/1
- Fa0/3
- Fa0/5
- Fa0/7
- Fa0/9
- Fa0/11
- Fa0/13
- Fa0/15
- Fa0/17
- Fa0/19
- Fa0/21
- Fa0/23

**VLAN 20 – VISITANTES**

Portas pares:
- Fa0/2
- Fa0/4
- Fa0/6
- Fa0/8
- Fa0/10
- Fa0/12
- Fa0/14
- Fa0/16
- Fa0/18
- Fa0/20
- Fa0/22
- Fa0/24

O mesmo padrão foi aplicado aos quatro switches de acesso.

## 4. Procedimentos de configuração

Primeiramente, foram criadas as VLANs 10 e 20 em cada switch de acesso.

### Criação das VLANs

```cisco
enable
configure terminal

vlan 10
name ALUNOS
exit

vlan 20
name VISITANTES
exit
```

### Configuração das portas ímpares – VLAN 10

```cisco
interface range fa0/1, fa0/3, fa0/5, fa0/7, fa0/9, fa0/11, fa0/13, fa0/15, fa0/17, fa0/19,
fa0/21, fa0/23
switchport mode access
switchport access vlan 10
exit
```

### Configuração das portas pares – VLAN 20

```cisco
interface range fa0/2, fa0/4, fa0/6, fa0/8, fa0/10, fa0/12, fa0/14, fa0/16, fa0/18, 
fa0/20, fa0/22, fa0/24
switchport mode access
switchport access vlan 20
exit
```

### Salvamento das configurações

```cisco
end
write memory
```

Os procedimentos foram aplicados nos quatro switches da camada de acesso.

## 5. Validação da configuração

Para verificar se as VLANs foram criadas corretamente e se as portas foram associadas
às respectivas VLANs, foi utilizado:

```cisco
show vlan brief
```

Também pode ser utilizado:

```cisco
show running-config
```

A validação permite conferir os IDs, nomes e interfaces associadas às VLANs.

## 6. Resultado

Ao final da configuração, os switches de acesso passaram a organizar os dispositivos
em duas VLANs distintas.

As portas ímpares foram destinadas à VLAN 10 (ALUNOS), enquanto as portas pares foram 
destinadas à VLAN 20 (VISITANTES).

A configuração permite a segmentação lógica da rede, facilitando sua organização e administração.

## 7. Conclusão

A atividade permitiu aplicar na prática os conceitos de VLANs e portas do tipo Access em 
uma infraestrutura de rede hierárquica, utilizando comandos Cisco IOS no ambiente de
simulação Cisco Packet Tracer.
