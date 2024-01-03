# LDAP

## Instalação

Para instalar o OpenLDAP no Debian, você pode seguir esses passos:

Atualize o índice de pacotes:

bash
Copy code
sudo apt update
Instale o OpenLDAP:

bash
Copy code
sudo apt install slapd ldap-utils
Durante a instalação, você será solicitado a definir a senha do administrador do LDAP (cn=admin,dc=example,dc=com). Defina uma senha forte para o administrador.

Reconfigure o OpenLDAP:

Se precisar reconfigurar o OpenLDAP após a instalação inicial, use o seguinte comando:

bash
Copy code
sudo dpkg-reconfigure slapd
Isso abrirá um assistente que permitirá reconfigurar o OpenLDAP.

Configuração adicional:

O assistente de configuração pode solicitar que você defina o domínio LDAP (por exemplo, dc=example,dc=com) e outras configurações básicas. Siga as instruções do assistente para configurar o OpenLDAP de acordo com suas necessidades.

Teste a instalação:

Use utilitários como ldapsearch para verificar se a instalação foi concluída com sucesso e se você pode fazer consultas ao servidor LDAP.

Essas etapas básicas devem ajudar a instalar o OpenLDAP no Debian. Após a instalação, você pode configurar a estrutura do LDAP, adicionar usuários, grupos e definir políticas de acesso conforme necessário para atender aos requisitos do seu ambiente.








## Configuração
Configuração
O arquivo de configuração[3] do serviço de diretório da suíte OpenLDAP (slapd) é o /etc/ldap/slapd.conf. Esse arquivo possui vários parâmetros que configuram desde a execução do serviço slapd até o backend de banco de dados que será utilizado, assim como os índices que devem ser gerados para agilizar as buscas e também a senha de administração para acessar o diretório. Ou seja, esse arquivo é a peça chave da implantação e sua configuração deve ser feita com bastante rigor. Devemos também nos certificar de que o acesso a esse arquivo estará restrito.

As seguintes regras, comuns aos arquivos de configuração de sistemas Unix, são válidas para o /etc/ldap/slapd.conf:

Linhas em branco e linhas começando com # são ignoradas.

Parâmetros e valores associados são separados por caracteres em branco (espaço ou tabulação).

Linhas com espaços em branco na primeira coluna serão consideradas como continuação da linha anterior.

Exemplo 2.1. Arquivo de configuração /etc/ldap/slapd.conf

####################### /etc/ldap/slapd.conf ######################
# Arquivo de configuração do serviço slapd.

# schema's
include         /etc/ldap/schema/core.schema
include         /etc/ldap/schema/cosine.schema
include         /etc/ldap/schema/nis.schema
include         /etc/ldap/schema/inetorgperson.schema

schemacheck     on

# serviço
pidfile         /var/run/slapd/slapd.pid
argsfile        /var/run/slapd/slapd.args

loglevel        296

modulepath      /usr/lib/ldap
moduleload      back_bdb

# segurança
allow           bind_v2

# bases de dados
backend         bdb
checkpoint 512 30

## base de dados no. 1
database        bdb
suffix          "dc=ime,dc=usp,dc=br"
directory       "/var/lib/ldap"
index           objectClass     eq
rootdn          "cn=admin,dc=ime,dc=usp,dc=br"
rootpw          {MD5}Xr4ilOzQ4PCOq3aQ0qbuaQ==
lastmod         on
mode            0600
cachesize       2000

## ACL's para a base de dados no. 1
access to attrs=userPassword
       by dn.base="cn=admin,dc=ime,dc=usp,dc=br" write
       by anonymous auth
       by self write
       by * none
access to * 
       by dn.base="cn=admin,dc=ime,dc=usp,dc=br" write
       by * read
###################################################################


https://jualabs.com/2015/07/03/instalacao-e-autenticacao-do-ldap-no-ubuntu-12-04/

Incluir o(s) nome(s) e o conteúdo do(s) arquivo(s) de configuração.

- Criar duas OU: `vendedores` e `rh`;
- Mover o grupo `sobrenome1` e seus membros para a OU `vendedores`;
- Mover os grupo `sobrenome2` e seus membros para a OU `rh`.

## Teste


