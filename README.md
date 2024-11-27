# Configuração Básica do VyOS

 Este arquivo contém um exemplo de configuração básica para o VyOS, incluindo configuração de interfaces, NAT, redirecionamento de portas e desativação de ping ICMP. 
## Comandos Básicos 
- **Entrar no modo de configuração**: `configure` 
- **Aplicar configurações**: `commit` 
- **Salvar configurações**: `save`
  > ⚠️ **Importante**Se não salvar, as configurações serão perdidas ao reiniciar o dispositivo.

## Configuração da Interface WAN (eth0)
```bash
set interfaces ethernet eth0 address x.x.x.x/x
set interfaces ethernet eth0 description WAN
set system name-server 1.1.1.1
set system name-server 8.8.8.8
edit protocols static route 0.0.0.0/0 next-hop x.x.x.x # Seria o gateway, que normalmente é informado pelo provedor de serviços de internet, sendo o mesmo responsável por fornecer o endereço IP.
```
## Configurar (eth1) Rede LAN
```bash
set interfaces ethernet eth1 address 192.168.0.1/24
set interfaces ethernet eth1 description LAN
```
## Masquerade WAN para LAN assim vai navegar
```bash
set nat source rule 10 description "Masquerade LAN para WAN"
set nat source rule 10 source address 192.168.0.0/24
set nat source rule 10 translation address "masquerade"
```
## Configurar redirecionamento de porta 
```bash
set nat destination rule 200 description "Redirecionar porta 30050 para 22"
set nat destination rule 200 destination port 30050
set nat destination rule 200 inbound-interface name eth0
set nat destination rule 200 protocol tcp
set nat destination rule 200 source address 201.222.31.205/32  #Regra opcional, só este ip externo que vai ter acesso a esta porta.
set nat destination rule 200 translation address 192.168.0.5  #IP da VM de destino
set nat destination rule 200 translation port 22 #Porta da VM
```
Cada regra tem que ter seu número ex:
>              set nat destination rule 200 description "Redirecionar porta 30050 para 22"
>              set nat destination rule 201 description "Redirecionar porta 80 para 80"
##Desativar ping 
```bash
set firewall global-options all-ping disable
```
