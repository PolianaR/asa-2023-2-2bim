# LDAP

## Instalação
```
sudo apt-get update
sudo apt-get install samba smbclient ldap-utils

```
Configurar o nome de nossa máquina com o nome de nosso dominio em: (nano /etc/hostname)

Você pode mudar temporariamente o nome da máquina usando o comando hostname. No entanto, esta mudança não será persistente após reinicialização.

Fazendo Backup do smb.conf:
Faça uma cópia de backup do arquivo smb.conf atual para garantir que você possa restaurá-lo se necessário:


`sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.bak`

Isso criará um arquivo de backup chamado smb.conf.bak.

3º - Configurando o Domínio com samba-tool:
Execute o comando samba-tool domain provision --use-rfc2307 --interactive para configurar o domínio do Samba interativamente:

```
sudo samba-tool domain provision --use-rfc2307 --interactive

```
Isso iniciará um processo interativo para configurar o domínio. Siga as instruções e forneça as informações necessárias, como nome do domínio, senha do administrador, etc.

4º - Configurando o smb.conf:
Após configurar o domínio, você precisará ajustar o arquivo smb.conf para refletir as configurações do seu domínio Samba. Abra o arquivo smb.conf em um editor de texto:


`sudo nano /etc/samba/smb.conf`

Edite o arquivo smb.conf de acordo com as necessidades do seu domínio Samba, adicionando configurações relevantes, compartilhamentos, permissões, etc.

Depois de editar o arquivo smb.conf, reinicie o serviço do Samba para aplicar as mudanças:

bash
```
sudo systemctl restart smbd
sudo systemctl restart nmbd

```

Certifique-se de revisar a documentação do Samba ou as informações específicas do seu ambiente para garantir que as configurações do smb.conf estejam de acordo com suas necessidades de domínio e compartilhamento de arquivos.


sudo hostname NOVO_NOME

Configuração adicional:


![img](../images/dominio-win7.png)

Teste a instalação:



## Configuração

Configuração

Incluir o(s) nome(s) e o conteúdo do(s) arquivo(s) de configuração.

- Criar duas OU: `vendedores` e `rh`;
![vendedores](../.png)
- Mover o grupo `sobrenome1` e seus membros para a OU `vendedores`;
- Mover os grupo `sobrenome2` e seus membros para a OU `rh`.

## Teste


