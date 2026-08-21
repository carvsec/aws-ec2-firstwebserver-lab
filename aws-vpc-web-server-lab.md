# Laboratório: Arquitetura de Rede AWS VPC, EC2, Apache com a Escola da Nuvem

Laboratório guiado durante o curso **Fundamentos de Computação em Nuvem AWS re/Start da Escola da Nuvem, com o objetivo de montar uma arquitetura de rede básica na AWS e subir um servidor web funcional dentro dela.

---

## Objetivo

Praticar os conceitos centrais de rede em nuvem, segmentação de sub-redes, controle de tráfego por Security Groups e provisionamento de instâncias, construindo, do zero, o ambiente que sustenta uma aplicação web simples.

---

## Arquitetura da VPC

| Recurso | Configuração |
|---|---|
| VPC (IPv4 CIDR) | `10.0.0.0/16` |
| Public Subnet 1 | `10.0.0.0/24` |
| Private Subnet 1 | `10.0.1.0/24` |
| Public Subnet 2 | `10.0.2.0/24` |
| Private Subnet 2 | `10.0.3.0/24` |
| Availability Zones | 2 |
| NAT Gateway | 1 (em uma AZ) |
| VPC Endpoints | Nenhum |
| Tenancy | Default |


---

## O que foi construído

1. **Criação da VPC e das sub-redes públicas e privadas**
   VPC `10.0.0.0/16` criada com quatro sub-redes duas públicas e duas privadas distribuídas em duas Availability Zones, isolando o que precisa de exposição à internet do que não precisa.

2. **Configuração de Security Groups**
   Regras de firewall aplicadas na instância, liberando explicitamente as portas necessárias para a operação do laboratório: **SSH (22)**, para acesso administrativo remoto, e **HTTP (80)**, para acesso ao servidor web. Qualquer outra porta permanece fechada por padrão — prática de menor privilégio aplicada à rede.

3. **Execução de instância EC2 com Amazon Linux**
   Provisionamento de uma instância `t3.micro` dentro da sub-rede pública, servindo como host do servidor web.

4. **Instalação e configuração de servidor Apache via SSH**
   Conexão remota via SSH na instância e instalação do Apache HTTP Server, deixando a página web acessível externamente através da porta liberada no Security Group.

---

## Conceitos praticados

- Planejamento de CIDR e segmentação de rede pública vs. privada como base de arquitetura segura por design
- Distribuição em múltiplas Availability Zones como fundamento de alta disponibilidade
- Security Groups como camada de controle de tráfego stateful firewall na borda da instância
- Acesso remoto seguro via SSH para administração de servidor
- Relação direta entre regra de rede Security Group e serviço exposto Apache na porta HTTP

---

## Observação sobre este writeup

A origem exata permitida nas regras do Security Group (se SSH estava restrito a um IP específico ou aberto) não foi registrada no momento do laboratório e não está incluída aqui por precisão. Em laboratórios futuros, o objetivo é salvar prints e configurações específicas durante a execução para produzir writeups com nível de detalhe técnico completo desde a regra de firewall até o resultado final.

---

*Laboratório realizado na Escola da Nuvem, trilha AWS re/Start.*
