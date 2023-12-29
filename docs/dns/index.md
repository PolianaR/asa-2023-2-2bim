# DNS

## Instalação
No Ubuntu/Debian, abra o terminal e execute os seguintes comandos:


```
sudo apt update
sudo apt install bind9
```

## Configuração
Configurando Zonas

Edite o arquivo named.conf para adicionar suas zonas. Por exemplo:



sudo nano /etc/bind/named.conf
Incluir o(s) nome(s) e o conteúdo do(s) arquivo(s) de configuração.

Cinco registros (4 pontos cada):

- 3 do tipo A (Endereços);
- 2 do tipo CNAME (`www` e `docs`);

## Teste
[Domain](https://github.com/PolianaR/asa-2023-2-2bim/blob/main/dominio%20no%20win7.png)
[Dns](

