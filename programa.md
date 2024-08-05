---
layout: page
title: Programa
subtitle: Introdução à Programação de Computadores para Biologia
#image: /img/hello_world.jpeg
---


## 2o semestre de 2024

**Horário:**    Terça-Feira – 10:00 às 12:00 horas

**Local:**    Sala de multimídia ou sala 05 - Centro didático  
                               
**Professora:** Tatiana Teixeira Torres, e-mail: tttorres(bio)ib.usp.br
OBS: substituir (bio) por @ 

## Programa:

| Aula | Data  | Tema                                            |
|------|-------|-------------------------------------------------|
| 1    | 06/08 | Apresentação da disciplina                      |
| 2    | 13/08 | Introdução à Programação / Bash                 |
| 3    | 20/08 | Bash (continuação) / Algoritmos                 |
| :x:  | 27/08 | Não haverá aula                                 |
| :x:  | 03/09 | Não haverá aula                                 |
| 4    | 10/09 | Introdução ao Perl / Variáveis e tipos de dados |
| 5    | 17/09 | Arrays e Hashes                                 |
| 6    | 24/09 | Estruturas de controle: condicionais            |
| 7    | 01/10 | Estruturas de controle: loops I                 |
| 8    | 08/10 | Estruturas de controle: loops II                |
| 9    | 15/10 | Manipulação de arquivos I                       |
| 10   | 22/10 | Manipulação de arquivos II                      |
| 11   | 29/10 | Manipulação de strings e expressões regulares   |
| 12   | 05/11 | Subrotinas                                      |
| 13   | 12/11 | Módulos I: introdução e CPAN                    |
| 14   | 19/11 | Módulos II: BioPerl                             |
| 15   | 03/12 | chatGPT e programação, revisão e encerramento   |

  

## Forma de avaliação:

Exercícios semanais: a cada novo tema de aula, será disponibilizado um exercício que deverá ser entregue no prazo de sete dias. A entrega dos exercícios será realizada via moodle (https://edisciplinas.usp.br/). O atraso na entrega implica na redução da nota pela metade. Serão 10 exercícios ao longo do semestre, com pesos diferentes conforme a complexidade do exercício. 

## Critério para aprovação e pesos das avaliações:

{% highlight perl linenos %}  
#!/usr/bin/perl

my ($E, $M, $H, $nota_final); #$E, easy; $M, medium; $H, hard
($E, $M, $H) = @ARGV; 

$nota_final = ((2*$E)+(3*$M)+(5*$H))/10;

if ($nota_final >= 5) {
  print "Aluno aprovado\n";
} else {
  print "Aluno reprovado\n";
}

#conversao de nota para conceitos, apenas para a Pos-graduacao
if ($nota_final < 5) {
  print "R, Reprovado, sem direito a credito\n";
} elsif ($nota_final <= 7.0) {
  print "C, Regular, com direito a credito\n";
} elsif ($nota_final <= 8.5) {
  print "B, Bom, com direito a credito\n";
} else {
  print "A, Excelente, com direito a credito\n";
}
exit;

{% endhighlight %}
  

## Bibliografia:

- Curtis Jamison, D. “Perl Programming for Biologists”, John Wiley & Sons, Inc., 2003.
- Wall, L.; Christiansen, T.; Orwant, J. “Programming Perl”, O'Reilly Media, 2000.
- Tisdall, J. “Beginning Perl for Bioinformatics”, O'Reilly Media, 2001.
- Setubal J. C.; Meidanis J. "Introduction to Computational Molecular Biology", Brooks/Cole Pub Co, 1997.
