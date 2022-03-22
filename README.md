# ServerDNSBind9
Implementação e Avaliação de um Serviço de DNS utilizando Bind9
---------------------------

Server DNS Ubuntun - Bind9

---------------------------
Configurações que iremos usar

REDE: 10.10.10.0/25
GATEWAY: 10.10.10.1
DNS: 10.10.10.3
HTTP: 10.10.10.4
VOIP: 10.10.10.5

Sudo su 

apt-get update

apt-get install bind9

Configurar Rede.

---------------------------

cd /etc/bind (Caminha até o diretório)
ls (listar os documentos na pasta acessada)

nano named.config.local

//zona direta (criando zona direta após abrir o arquivo) <br>
zone "name.example.com" { <br>
	type master; <br>
	file "/etc/bind/db.name.example.com"; <br>
}; <br>


//zona reversa <br>
zone "10.-in.addr.arpa" { <br>
	type master; <br>
	file "/etc/bind/db.10"; <br>
}; <br>

Pronto Zonas Criadas.!
Configurações iniciais feitas

---------------------------

Agora criar os arquivos das Zonas 
(Zona direta, arquivo padrao db.local)
(Zona reversa, arquivo padrao db.127)

cp db.local db.name.example.com
cp db.127 db.10

ls (listar os novos arquivos das zonas)

---------------------------
Agora vamos editar os arquivos das zonas 

//ZONA DIRETA
nano db.name.example.com

Mudar o dominio dos arquivos de configurações


localhost pelo nome do novo dominio name.example.com
(Muda em dois locais em cima, um embaixo)

Troca o endereço IP - 127.0.0.1 por 10.10.10.3

Identificação do Endereço IPv6 - apaga (nao irá usar Ultima linha)

---------------------------

ADD

WWW	IN	A	10.10.10.4 <br>
ftp	IN	A	10.10.10.4 <br>	
voip	IN	A	10.10.10.5 <br>

Feito isso salvar e sair do nano		

---------------------------
//ZONA REVERSA
nano db.10
  
Troca os localhost por name.example.com

//Agora em -> 1.0.0 IN	PTR name.example.com

//substitui pelo resto do Endereço IP (só que ao contrario)
3.10.10

//Feito isso Agora restart o bind9 - 

service bind9 restart (usar esse!)

/etc/init.d/bind9 restart (restarta)
/etc/init.d/bind9 status (ver o status)

---------------------------
Editar o arquivo de resolvedor de nomes da maquina

nano /etc/resolv.conf 

ADD name serve 

nameserver 10.10.10.3   (Save , exit).

---------------------------

AGORA É TESTAR !!!

host name.example.com <br>
nslookup name.example.com <br>
host www.name.example.com <br>
host ftp.name.example.com <br>
host voip name.example.com <br>
nslookup voip.name.example.com <br>







