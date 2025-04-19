# projeto-docker-DIO

//Criação de Banco de Dados
CREATE TABLE dados (
    ClienteID int,
    Nome varchar(50),
    Sobrenome varchar(50),
    Endereco varchar(150),
    Cidade varchar(50),
    Host varchar(50)
);

//configuração PHP
<html>
<head>
<title>PHP</title>
</head>
<body>
<?php
ini_set("display_errors", 1);
header('Content-Type: text/html; charset=iso-8859-1');
echo 'Versao Atual do PHP: ' . phpversion() . '<br>';
$servername = "192.168.15.5";
$username = "root";
$password = "Passwd456";
$database = "meubanco";
// Criar conexão
$link = new mysqli($servername, $username, $password, $database);
/* check connection */
if (mysqli_connect_errno()) {
    printf("Connect failed: %s\n", mysqli_connect_error());
    exit();
}
$valor_rand1 =  rand(1, 999);
$valor_rand2 = strtoupper(substr(bin2hex(random_bytes(4)), 1));
$host_name = gethostname();
$query = "INSERT INTO dados (ClienteID, Nome, Sobrenome, Endereco, Cidade, Host) VALUES ('$valor_rand1' , '$valor_rand2', '$valor_rand2', '$valor_rand2', '$valor_rand2','$host_name')";
if ($link->query($query) === TRUE) {
  echo "New record created successfully";
} else {
  echo "Error: " . $link->error;
}
?>
</body>
</html>

//Configuração Proxy
http {
   
    upstream all {
        server 172.31.0.47:80;
        server 172.31.0.139:80;
        server 172.31.0.119:80;
    }

    server {
         listen 4500;
         location / {
              proxy_pass http://all/;
         }
    }

}

events { }
