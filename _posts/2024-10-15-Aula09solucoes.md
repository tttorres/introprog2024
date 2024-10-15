---
layout: post
title: Aula 09 com soluções
#image: /img/hello_world.jpeg
---
# Exercícios (algoritmos e programação)

## Exercício 01

Escreva um script que peça ao usuário para inserir uma quantidade indefinida de números como argumentos na linha de comando. O script deverá calcular a média aritmética desses números e retornar na saída padrão.

### Solução:
{% highlight perl linenos %}
#!usr/bin/perl

# Verifica se há argumentos
if (@ARGV == 0) {
    die "Por favor, insira numeros como argumentos na linha de comando.\n";
}

$soma = 0;
$quantidade = @ARGV;

# Itera sobre os argumentos e calcula a soma e a quantidade
foreach $numero(@ARGV) {
	$soma += $numero;   # Soma cada nomero
}

# Calcula a média 
my $media = $soma / $quantidade;
print "A média aritmética é: $media\n";

exit;
{% endhighlight %}

========


## Exercício 02

Faça um script que peça uma string na linha de comando e verifique se a string é um palíndromo (mesma leitura da frente para trás e vice-versa). O comando reverse() inverte qualquer string.

### Solução:
{% highlight perl linenos %}
#!usr/bin/perl

# Verifica se há argumentos
if (@ARGV == 0) {
    die "Por favor, insira uma string.\n";
}

$str = $ARGV[0];

# Inverte a string
$str_reversa = reverse($str);

# Compara a string original com a invertida
if ($str eq $str_reversa) {
    print "É um palíndromo.\n";
} else {
    print "Não é um palíndromo.\n";
}

exit;
{% endhighlight %}

========


## Exercício 03

Escreva um script que converta uma temperatura em Celsius informada na linha de comando para Fahrenheit.

### Solução:
{% highlight perl linenos %}
#!usr/bin/perl

# Verifica se há argumentos
if (@ARGV == 0) {
    die "Por favor, informe uma temperaura em Celcius.\n";
}

$celsius = $ARGV[0];

$fahrenheit = ($celsius * 9/5) + 32;

print "Temperatura em Fahrenheit: $fahrenheit\n";

exit;
{% endhighlight %}

========


## Exercício 04

Crie um script que conte o número de adeninas (A), timinas (T), citosinas (C) e guaninas (G) em uma sequência de DNA fornecida pelo usuário.

### Solução:
{% highlight perl linenos %}
#!usr/bin/perl

# Verifica se há argumentos
if (@ARGV == 0) {
    die "Por favor, informe uma sequencia de DNA.\n";
}

$seq = $ARGV[0];

#inicializando um hash com a contagem de cada nucleotideo
%count = ('A' => 0, 
     	  'T' => 0, 
          'C' => 0, 
          'G' => 0);
		  
#quebrando a sequencia do usuario em um array
@sequencia = split('', $seq);

#passando por cada nucleotideo da sequencia e aumentando a contagem
foreach $nucletideo (@sequencia) {
    $count{$nucletideo}++;
}

print "A: $count{'A'}, T: $count{'T'}, C: $count{'C'}, G: $count{'G'}\n";

exit;
{% endhighlight %}

========


## Exercício 05

Escreva um script que gere uma senha aleatória de 10 caracteres usando letras e números. A função rand() pode ser utilizada para gerar um número aleatório entre 0 e o número indicado como parâmetro. O operador "." faz a concatenação de strings ou caracteres.

### Solução:
{% highlight perl linenos %}
#!usr/bin/perl

# Criando um array de caracteres para o sorteio
@caracteres = ('A'..'Z', 'a'..'z', 0..9);
$tamanho_senha = 10;
$senha = '';

for (1..$tamanho_senha) {

    $indice = int(rand(@caracteres));  # Gera um índice aleatório de 0 ao úlimo elemento do array
    $senha .= $caracteres[$indice];    # Concatena o caractere correspondente
	
} 

print "Senha gerada: $senha\n";

exit;
{% endhighlight %}

========


## Exercício 06

Crie um script que converta um arquivo FASTQ para o formato CSV, onde cada linha tem o identificador da sequência, a sequência de nucleotídeos e a qualidade separados por vírgulas.

Arquivo em formato fastq para testar o script: [chom.txt](/introprog2024/files/chom.txt)  
MD5 = 3e6bc3fd47c39af9ba091edc0c6e5d31

### Solução:
{% highlight perl linenos %}
#!usr/bin/perl

# Verifica se o nome do arquivo foi passado como argumento
if (@ARGV != 2) {
    die "Uso: perl $0 <input.fasta> <output.csv>\n";
}

($input_file, $output_file) = @ARGV;

# Abre o arquivo de entrada FASTQ para leitura
open(IN, "<$input_file") or die "Não foi possível abrir $input_file\n";

# Abre o arquivo de saída CSV para escrita
open(OUT, ">$output_file") or die "Não foi possível abrir $output_file\n";

# Inicializa variáveis
$id = '';
$sequencia = '';
$qualidade = '';

# Lê o arquivo FASTQ
while (<IN>) {
    chomp $_;
    # Leitura das linhas no formato FASTQ
    if ($. % 4 == 1) {        # resto 1: Linha do identificador
        $id = substr($_, 1);  # Remove o '@' do início
    } elsif ($. % 4 == 2) {   # resto 2: Linha da sequência
        $sequencia = $_;
    } elsif ($. % 4 == 0) {   # resto 0: Linha da qualidade
        $qualidade = $_;
        # Quando temos todos os dados, escrevemos no CSV
        print OUT "$id,$sequencia,$qualidade\n";
    }
}

# Fecha os arquivos
close($in);
close($out);

exit;
{% endhighlight %}

========


## Exercício 07

Implemente o jogo de "Pedra, Papel e Tesoura". O jogador escolhe uma das três opções, e o computador sorteia aleatoriamente. O programa deve determinar quem ganhou ou se houve empate, repetindo até que o jogador decida sair.

### Solução:
{% highlight perl linenos %}
#!/usr/bin/perl

# Definições das escolhas possíveis
@opcoes = ("pedra", "papel", "tesoura");

# Loop principal do jogo
while (1) {
    print "Escolha pedra, papel ou tesoura (ou 'sair' para terminar): ";
    $escolha_jogador = <STDIN>;
    chomp($escolha_jogador);

    if ($escolha_jogador eq "sair") { last } 

    # Escolha do computador
    $sorteio = int(rand(3));
    $escolha_computador = $opcoes[$sorteio];

    print "Computador escolheu: $escolha_computador\n";

    # Determina o vencedor
    if ($escolha_jogador eq $escolha_computador) {
        print "Empate!\n";
    } elsif (($escolha_jogador eq "pedra") && ($escolha_computador eq "tesoura")) {
        print "Você venceu!\n";
    } elsif (($escolha_jogador eq "papel") && ($escolha_computador eq "pedra")) {    
        print "Você venceu!\n";
    } elsif (($escolha_jogador eq "tesoura") && ($escolha_computador eq "papel")) {
        print "Você venceu!\n";
    } else {
        print "Você perdeu!\n";
    }
}

exit;
{% endhighlight %}

========


## Exercício 08

Escreva um script em Perl que faça o seguinte que abra um arquivo em texto para leitura, conte o número de linhas, palavras e caracteres e mostre o resultado na saída padrão.

### Solução:
{% highlight perl linenos %}
#!/usr/bin/perl

# Verifica se o nome do arquivo foi passado como argumento
if (@ARGV == 0) {
    die "Uso: perl $0 <input.fasta>\n";
}

$input_file = $ARGV[0];

# Abre o arquivo de entrada FASTA para leitura
open(SEQ, "<$input_file") or die "Não foi possível abrir $input_file\n";

# Inicializa contadores
$linhas = 0;
$palavras = 0;
my $caracteres = 0;

while (<SEQ>) {
    chomp $_;
    $linhas++;                              # conta linhas
    $palavras += scalar(split(/\s+/, $_));  # Conta palavras
    $caracteres += length($linha);          # Conta caracteres
}

close(SEQ);

# Escreve o resultado na saida padrao
print "Numero de linhas: $linhas\n";
print "Numero de palavras: $palavras\n";
print "Numero de caracteres: $caracteres\n";

exit;
{% endhighlight %}

========


## Exercício 09

Modifique o script criado no exercício 04 para contar o número de adeninas (A), timinas (T), citosinas (C) e guaninas (G) em um arquivo de sequências de DNA em formato FASTA. O script deverá retornar a frequência de A, T, C e G no genoma (no arquivo todo) e retornar na saída padrão. 

Arquivo em formato fasta para testar o script: [dmel-gene-r5.45.fasta](/introprog2024/files/dmel-gene-r5.45.fasta)  
MD5 = 185057f6340dc01e022cbbbc7a51f343

### Solução:
{% highlight perl linenos %}
#!/usr/bin/perl

# Verifica se um arquivo foi fornecido como argumento
if (@ARGV != 1) {
    die "Uso: perl $0 arquivo.fasta\n";
}

$filename = $ARGV[0];

# Inicializa contadores para A, T, C e G
$count_A = 0;
$count_T = 0;
$count_C = 0;
$count_G = 0;

# Abre o arquivo FASTA
open(FASTA, "<$filename") or die "Não foi possível abrir o arquivo $filename";

while (<FASTA>) {
    chomp $_;
    
    # Converte a linha em um array de caracteres
    @nucleotideos = split(//, $_);
    
    # Ignora linhas de cabeçalho (que começam com ">")
    if ($nucleotideos[0] eq ">") {
        next;
    }
    
    # Percorre cada nucleotídeo da linha e incrementa o contador correspondente
    foreach my $nucleotideo (@nucleotideos) {
        if ($nucleotideo eq 'A') {
            $count_A++;
        } elsif ($nucleotideo eq 'T') {
            $count_T++;
        } elsif ($nucleotideo eq 'C') {
            $count_C++;
        } elsif ($nucleotideo eq 'G') {
            $count_G++;
        }
    }
}

close(FASTA);

# Calcula o total de nucleotídeos
my $total_nucleotideos = $count_A + $count_T + $count_C + $count_G;

# Calcula a frequência relativa de cada nucleotideo 
$freq_A = ($count_A / $total_nucleotideos) * 100;
$freq_T = ($count_T / $total_nucleotideos) * 100;
$freq_C = ($count_C / $total_nucleotideos) * 100;
$freq_G = ($count_G / $total_nucleotideos) * 100;

# Imprime a frequência relativa de cada nucleotideo 
print "Frequência relativa:\n";
print "Adenina (A): $freq_A\n";
print "Timina (T): $freq_T\n";
print "Citosina (C): $freq_C\n";
print "Guanina (G): $freq_G\n";

exit;
{% endhighlight %}

========


## Exercício 10

Crie um script que leia duas sequências de nucleotídeos de mesmo tamanhos fornecidas pelo usuário e determine o percentual de similaridade entre elas. A cada nucleotídeo idêntico, é adicionado um ponto de similaridade. 

### Solução:
{% highlight perl linenos %}
#!/usr/bin/perl

# Solicitar as duas sequências ao usuário
print "Digite a primeira sequência de nucleotídeos: ";
$seq1 = <STDIN>;
chomp($seq1);

print "Digite a segunda sequência de nucleotídeos: ";
$seq2 = <STDIN>;
chomp($seq2);

# Transformando as sequencias em arrays
@sequencia1 = split(//, $seq1);
@sequencia2 = split(//, $seq2);

# Calculando a similaridade
$matches = 0;

for ($i = 0; $i < length($seq1); $i++) {
	
    if ($sequencia1[$i] eq $sequencia2[$i]) {
		++$matches;
	}
}

$percentual = ($matches / length($seq1)) * 100;
print "O percentual de similaridade é: $percentual%\n";

exit;
{% endhighlight %}

========


## Exercício 11

Você está simulando populaçoes de um organismo diplóide com diferente frequências de alelos. Imagine que há dois alelos, A e a, e você deseja criar um conjunto de genótipos para 10 indivíduos. Os genótipos possíveis são AA, Aa, e aa. Escreva um script que sorteie aleatoriamente o genótipo de cada indivíduo e mostre no final a contagem de cada genótipo e as frequências alélicas.

### Solução:
{% highlight perl linenos %}
#!/usr/bin/perl

# Numero de indivíduos na populacao
$num_individuos = 10;

# Contadores para cada genotipo
$count_AA = 0;
$count_Aa = 0;
$count_aa = 0;

# Sorteio aleatório de genótipos
for (1..$num_individuos) {
    # Gera um número aleatório entre 0 e 2
    $genotipo = int(rand(3)); # 0 -> AA, 1 -> Aa, 2 -> aa

    if ($genotipo == 0) {
        $count_AA++;
    } elsif ($genotipo == 1) {
        $count_Aa++;
    } elsif ($genotipo == 2) {
        $count_aa++;
    }
}

# Contagem total de genotipos
$total_genotipos = $count_AA + $count_Aa + $count_aa;

# Calculo das frequencias alelicas
$frequencia_A = ($count_AA * 2 + $count_Aa) / ($total_genotipos * 2);
$frequencia_a = ($count_aa * 2 + $count_Aa) / ($total_genotipos * 2);

# Impressao dos resultados
print "Contagem de genotipos:\n";
print "AA: $count_AA\n";
print "Aa: $count_Aa\n";
print "aa: $count_aa\n\n";

print "Frequências alélicas:\n";
print "Frequência de A: $frequencia_A\n";
print "Frequência de a: $frequencia_a\n";

exit;
{% endhighlight %}

========


## Exercício 12

Implemente o jogo da forca. O computador deve escolher uma palavra secreta, e o jogador precisa adivinhar uma letra por vez. O jogador tem um número limitado de tentativas antes de "ser enforcado". Exiba o progresso do jogador, mostrando as letras corretas e marcando as letras ainda desconhecidas com underscores (_).

### Solução:
{% highlight perl linenos %}
#!/usr/bin/perl

# Definindo a palavra secreta
@palavra_secreta = split(//, "perl");
@palavra_exibida = qw(_ _ _ _);

print "\n\@palavra_secreta eh @palavra_secreta\n";

$max_tentativas = 6;
$tentativas = 0;
$acertos = 0;

print "Bem-vindo ao Jogo da Forca!\n";

while ($tentativas < $max_tentativas && $acertos < @palavra_exibida) {
    print "\nPalavra: @palavra_exibida\n";
    
    $tentativas_restantes = $max_tentativas - $tentativas;
    $encontrado = 0;
    
    print "Tentativas restantes: $tentativas_restantes\n";
    print "Insira uma letra: ";
  
    $palpite = <STDIN>;
    chomp($palpite);  # Remove a nova linha do input

    # Verifica se a letra está na palavra secreta
    
    for ($i = 0; $i < @palavra_secreta; $i++) {
				
	if ($palavra_secreta[$i] eq $palpite) {
            $palavra_exibida[$i] = $palpite;  # Atualiza a letra na palavra exibida
            ++$acertos; 
            $encontrado = 1;                  # Atualiza encontrado fica verdadeiro
        }
    }
    
    # Se a letra não está na palavra, incrementa o contador de tentativas
    unless($encontrado) { 
        $tentativas++;
        print "A letra '$palpite' não está na palavra. Você perdeu uma tentativa!\n";
    }
}

# Resultado final

$palavra_secreta = join('', @palavra_secreta);
$palavra_exibida = join('', @palavra_exibida);

if ($palavra_exibida eq $palavra_secreta) {
    print "\nParabéns! Você adivinhou a palavra: $palavra_secreta\n";
} else {
    print "\nVocê foi enforcado! A palavra era: $palavra_secreta\n";
}

exit;
{% endhighlight %}

========
