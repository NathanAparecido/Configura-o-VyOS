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
## Configurar eth1 Rede LAN
```bash
set interfaces ethernet eth1 address 192.168.0.1/24
set interfaces ethernet eth1 description LAN
```
