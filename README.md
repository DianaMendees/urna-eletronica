#Projeto feito no curso de internet escola Cedup-diomicio freitas
#turma 202
urna eletronica

<?php
session_start();

$visor=@$_GET['digito'];
$_SESSION['votacao'] = @$_SESSION['votacao'] . $visor ;
$contbranco=null;
$contnulo=null;

if(((@$_GET['campo']==13) || (@$_GET['campo']==45) || (@$_GET['campo']==24)) && (@$_GET['confirmar']=='confirmar') ){
	$voto = $_SESSION['votacao'];
	$arquivo= "urna.txt";
	$conteudo ="-".$voto;
	$abertura=fopen("$arquivo","a+");
	$gravacao=fwrite($abertura, $conteudo);
	fseek($abertura,0);
	$leitura=fread($abertura,filesize($arquivo));
	fclose($abertura);
	echo $leitura;
	unset ($_SESSION['votacao']);
}else if((@$_GET['campo']=='') && (@$_GET['confirmar']=='confirmar')){
	$contbranco = @$_SESSION['branco'] + 1;
	$_SESSION['branco'] = $contbranco;
	$arquivo= "branco.txt";
	$conteudo = $contbranco;
	$abertura=fopen("$arquivo","w");
	$gravacao=fwrite($abertura, $conteudo);
	fseek($abertura,0);
	$leitura=fread($abertura,filesize($arquivo));
	fclose($abertura);
	unset ($_SESSION['votacao']);
}else if(((@$_GET['campo']!=13) || (@$_GET['campo']!=45) || (@$_GET['campo']!=24)) && (@$_GET['confirmar']=='confirmar') ){
	$contnulo = @$_SESSION['digito'] +1;
	$_SESSION['digito'] = $contnulo;
	$arquivo= "nulo.txt";
	$conteudo =$contnulo;
	$abertura=fopen("$arquivo","w");
	$gravacao=fwrite($abertura, $conteudo);
	fseek($abertura,0);
	$leitura=fread($abertura,filesize($arquivo));
	fclose($abertura);
	unset ($_SESSION['votacao']);
}
?>
<!DOCTYPE HTML>
<html lang="en-US">
<head>
	<meta charset="UTF-8">
	<title></title>
</head>
<body>
	
	<form action="" method="get">
	
	<div>
	<table border='0' height="3" width="3">
	<tr>
		<input type="text" name="campo"  value="<?php echo @$_SESSION['votacao']; ?>" />
		</tr>
	
	<tr>
		<td><input type="submit"  name="digito" value="1" /></td>
		<td><input type="submit"  name="digito" value="2" /></td>
		<td><input type="submit"  name="digito" value="3" /> </td>
	</tr>
	<tr>
		<td><input type="submit" name="digito"  value="4" /></td>
		<td><input type="submit" name="digito"  value="5" /></td>
		<td><input type="submit" name="digito"  value="6" /></td>
	</tr>
	<tr>
		<td><input type="submit" name="digito"  value="7" /></td>
		<td><input type="submit" name="digito"  value="8" /></td>
		<td><input type="submit" name="digito"  value="9" /></td>
	</tr>
	
	<tr>
	
		<td><input type="reset"  value="cancelar" name="cancelar"/></td>
		<td><input type="submit"   value="branco" name="branco" onclick="urna.digito.value +=''" /></td>
		<td><input type="submit"    value="confirmar" name="confirmar"/></td>
	</tr>
	
	</table>
	</div>
	</form>
	<div> 
		<h2>Legenda</h2>
		<p>13-Dilma</p>
		<p>45-Aecio</p>
		<p>24-Joaquim</p>
	</div>

</body>
</html>

