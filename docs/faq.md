# Perguntas frequentes (FAQ)

Dúvidas que aparecem na prática, respondidas direto. Cada resposta aponta para o
capítulo que trata do assunto a fundo.

## Por que meu leitor não lê a tag?

Quase sempre é um destes três:

1. Frequência errada. O leitor é de uma faixa e a tag é de outra. LF e HF não se
   enxergam. Teste as duas antes de concluir que a tag está morta.
2. Posição. O acoplamento cai muito fora do centro. Deslize a credencial pela
   superfície, teste as duas faces e incline um pouco. A maioria das não-leituras
   some com um ajuste de poucos milímetros.
3. Você está lendo um emulador com outro leitor. Dois circuitos ativos se acoplam
   mal. Use a tag física passiva.

Detalhe em [cap. 01](01-fundamentos.md) e [cap. 02](02-anatomia-interna.md).

## Qual a diferença entre UID de 4 bytes e de 7 bytes?

É o tamanho do número de série da tag. O que importa na prática: para copiar uma
credencial, o tamanho do UID do destino tem que casar com o da origem, porque o
bloco 0 (onde o UID mora) tem layout diferente para cada tamanho. Misturar 4 e 7
bytes dá erro de tamanho de UID. Ver [cap. 04](04-alta-frequencia-hf.md).

## O que é um cartão "mágico"?

É uma credencial HF em branco cujo bloco 0 pode ser reescrito, ou seja, dá para
mudar o UID. Cartões comuns têm o bloco 0 travado de fábrica. Os Magic existem
justamente para permitir cópia. Ver [cap. 06](06-cartoes-magic.md).

## Gravei, mas o UID continua o mesmo. Por quê?

O bloco 0 está travado. O cartão não é Magic de verdade, ou é um Magic
grava-uma-vez que já foi usado. A saída é trocar o destino por um Magic com bloco
0 regravável (Geração 1 é o mais seguro). E sempre releia depois de gravar. Ver
[cap. 08](08-erros-comuns.md).

## Como sei se um sistema só usa o UID?

Leia o dump. Se todos os dados estão em 00 e todas as chaves são o padrão FF, o
cartão não guarda nada além do número de série. O sistema libera o acesso só pelo
UID. Isso se chama UID-only e torna a cópia simples: basta reproduzir o UID num
destino que aceite gravar o bloco 0. Ver [cap. 05](05-mifare-classic.md).

## Dá para reescrever o ID de um EM4100?

Não. O EM4100 é só de leitura, com ID fixo de fábrica. Para copiar um ID de LF
você precisa gravar num transponder regravável (por exemplo o T5577), que aceita
escrita e consegue emular o EM4100. Ver [cap. 03](03-baixa-frequencia-lf.md).

## Como eu "perco" uma tag?

Dois jeitos clássicos:

1. Escrever o UID errado num Magic grava-uma-vez, que trava o bloco 0 com valor
   errado para sempre.
2. Zerar um Classic escrevendo tudo em 00, incluindo os access bits. Um padrão de
   access inválido trava o setor.

Prevenção: prefira Magic Geração 1 (regravável), nunca force uma gravação quando a
ferramenta avisar incompatibilidade, e ao resetar grave os trailers com o padrão
de fábrica, nunca tudo em 00. Ver [cap. 08](08-erros-comuns.md).

## O SAK diz o tipo com certeza?

Não. O SAK é a pista rápida da família, mas chips mágicos e variações podem mostrar
o mesmo SAK de um chip comum. Confirme cruzando SAK com ATQA, tamanho de UID e
comportamento. Ver [cap. 04](04-alta-frequencia-hf.md).

## O formato (chaveiro, cartão, adesivo) indica o tipo?

Não. O formato físico não diz nada sobre o chip. Um chaveiro, um cartão e um
adesivo podem ter o mesmo chip, e dois chaveiros iguais por fora podem ser de
frequências diferentes. Só a leitura revela o que há dentro. Ver
[cap. 02](02-anatomia-interna.md).

## A ferramenta leu EM4100, mas a cópia se comporta estranho. Por quê?

Um transponder regravável (como o T5577) pode estar configurado para imitar o
EM4100. O rótulo lido reflete o protocolo emulado, não necessariamente o chip
real. Valide testando escrita e releitura. Ver [cap. 03](03-baixa-frequencia-lf.md)
e [cap. 08](08-erros-comuns.md).

## Por onde começo se nunca mexi com isso?

Leia na ordem, do [cap. 01](01-fundamentos.md) ao [cap. 10](10-dispositivos-leitura.md).
Se já tem uma credencial na mão, vá ao
[fluxograma mestre (cap. 07)](07-metodologia-identificacao.md). Para consulta
rápida, use a [referência rápida](referencia-rapida.md).

Voltar ao [índice (README)](../README.md).
