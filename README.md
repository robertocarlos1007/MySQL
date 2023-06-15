# MySQL
login.php

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tela de login</title>
    <style>
      body {
        font-family: Arial, Helvetica, sans-serif;
        background-image: linear-gradient(45deg,cyan, yellow);
      }
      
      div {
        background-color: rgba(0, 0, 0,0.9);
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%,-50%);
        padding: 80px;
        border-radius: 15px;
        color: white;
      }
       
      input {
        padding: 15px;
        border: none;
        outline: none;
        font-size: 15px;
      }
      
      #entrar {
        display: block;
        margin: 0 auto;
        width: 150px;
        height: 40px;
        cursor: pointer; /* Adicionando efeito de mãozinha ao cursor */
      }
      
      @keyframes neon-border {
        0% {
          border-color: #ff00ff;
        }
        50% {
          border-color: #ff00ff;
        }
        100% {
          border-color: #ff00ff;
        }
      }
    </style>
</head>
<body>
    
<div>
    <h1>LOGIN</h1>
    <form name="login" action="logado.php" method="POST">
        Login: <input type="text" name="login" required placeholder="Digite seu login...">
        <br><br>
        Senha: <input type="password" name="senha" required placeholder="Digite sua senha...">
        <br><br>
        <input type="submit" id="entrar" value="Entrar">
    </form>
</div>

<script>
    function getRandomColor() {
        const letters = "0123456789ABCDEF";
        let color = "#";
        for (let i = 0; i < 6; i++) {
            color += letters[Math.floor(Math.random() * 16)];
        }
        return color;
    }

    const divElement = document.querySelector("div");
    divElement.style.borderColor = getRandomColor();
</script>

</body>
</html>

-------------------------------------------------------------

conexao.php


<?php

$conexao = mysqli_connect('localhost', 'root','', 'projetoa3', '3306');

if(!$conexao){
   die("erro de conexão");
}
?>

-------------------------------------------------------------

logado.php

<?php

include('conexao.php');
$login = isset($_POST['login']) ? $_POST['login'] : '';
$senha = isset($_POST['senha']) ? $_POST['senha'] : '';

$select = "SELECT nome, login, senha from login where login = '$login' and senha = '$senha' " ;
$execute = mysqli_query($conexao, $select);
$dados = mysqli_fetch_row($execute);

if($login == $dados[1] && $senha == $dados[2]){
    session_start();
    $_SESSION['nome'] = $dados[0];
   header('location: index.php');

}else{
    header('location: login.php');
}

?>

-------------------------------------------------------------

index.php

<?php
session_start();
?>
<html>
<head>
    <style>
      body{
        font-family: Arial, Helvetica, sans-serif;
        background-image: linear-gradient(45deg,cyan, yellow);
      }
      div{
        background-color: rgba(0, 0, 0,0.9);
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%,-50%);
        padding: 80px;
        border-radius: 15px;
        color: white;
      }
       
      input{
        padding: 15px;
        border: none;
        outline: none;
        font-size: 15px;
      }
      
      @keyframes neon-border {
        0% {
          border-color: #ff00ff;
        }
        50% {
          border-color: #ff00ff;
        }
        100% {
          border-color: #ff00ff;
        }
      }
    </style>
</head>
<body>
    <div>
        Olá, seja bem-vindo <?php
        if (isset($_SESSION['nome']) == null){
            ?> visitante<br>
            Realize o <a href="login.php">login</a>
        <?php } else {
            echo $_SESSION['nome']; ?><br><br>
            Para cadastrar um novo usuário, clique em: <a href="cadastrar.php"><h3>cadastrar</h3></a>
            Para finalizar a sessão, clique em: <a href="logout.php"><h3>sair</h3></a>
        <?php } ?>
    </div>

    <script>
        function getRandomColor() {
            const letters = "0123456789ABCDEF";
            let color = "#";
            for (let i = 0; i < 6; i++) {
                color += letters[Math.floor(Math.random() * 16)];
            }
            return color;
        }

        const divElement = document.querySelector("div");
        divElement.style.borderColor = getRandomColor();
    </script>
</body>
</html>

-------------------------------------------------------------

cadastrar.php

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tela de Cadastro</title>
    <style>
      body {
        font-family: Arial, Helvetica, sans-serif;
        background-image: linear-gradient(45deg,cyan, yellow);
      }
      
      div {
        background-color: rgba(0, 0, 0,0.9);
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%,-50%);
        padding: 80px;
        border-radius: 15px;
        color: white;
      }
       
      input {
        padding: 15px;
        border: none;
        outline: none;
        font-size: 15px;
      }
      
      #cadastrar {
        display: block;
        margin: 0 auto;
      }
      
      @keyframes neon-border {
        0% {
          border-color: #ff00ff;
        }
        50% {
          border-color: #ff00ff;
        }
        100% {
          border-color: #ff00ff;
        }
      }
    </style>
</head>
<body>
    <div>
        <h3>Digite as seguintes informações</h3>
        <form id="cadastro" action="cadastro.php" method="post">
            nome: <input type="text" name="nome" required placeholder="Digite seu nome"><br><br>
            login: <input type="text" name="login" required placeholder="Digite seu login"><br><br>
            senha: <input type="password" name="senha" required placeholder="Digite sua senha"><br><br>
            <input type="submit" id="cadastrar" value="Cadastrar">
        </form>
    </div>

    <script>
      function getRandomColor() {
        const letters = "0123456789ABCDEF";
        let color = "#";
        for (let i = 0; i < 6; i++) {
          color += letters[Math.floor(Math.random() * 16)];
        }
        return color;
      }
  
      const divElement = document.querySelector("div");
      divElement.style.borderColor = getRandomColor();
    </script>
</body>
</html>

-------------------------------------------------------------

cadastro.php

<?php
include("conexao.php");

$nome = isset($_POST['nome']) ? $_POST['nome'] : '';
$login = isset($_POST['login']) ? $_POST['login'] : '';
$senha = isset($_POST['senha']) ? $_POST['senha'] : '';

// Verifica se o login já existe no banco de dados
$verificaLogin = "SELECT * FROM login WHERE login = '$login'";
$result = mysqli_query($conexao, $verificaLogin);

if (mysqli_num_rows($result) > 0) {
    echo "Este login já está em uso. Por favor, escolha outro login.";
} else {
    $insert = "INSERT INTO login (nome, login, senha) VALUES ('$nome', '$login', '$senha')";
    $query = mysqli_query($conexao, $insert);
    header('location: index.php');
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tela de Cadastro</title>
    <style>
        body {
            font-family: Arial, Helvetica, sans-serif;
            background-image: linear-gradient(45deg, violet, black);
        }
    </style>
</head>
<body>

</body>
</html>

-------------------------------------------------------------

logout.php

<?php
session_start();
$_SESSION['nome'] = null;
session_destroy();
header('location: index.php');
?>
