# Referência rápida (cheat sheet)

Uma página só de tabelas, para consulta na hora de identificar uma credencial sem
reler o capítulo inteiro. Cada tabela aponta para o capítulo onde o assunto está
detalhado.

## Frequências

| Faixa | Frequência | Alcance passivo | Dados | Uso comum |
|---|---|---|---|---|
| LF | 125 kHz (às vezes 134) | alguns cm | só um ID, em geral | acesso legado, rastreio animal, imobilizador |
| HF | 13,56 MHz | milímetros a cerca de 10 cm | setores, arquivos, cripto | crachás, transporte, pagamento, NFC |

LF e HF não se enxergam. Antena de uma faixa não lê a outra. Ver
[cap. 01](01-fundamentos.md).

## SAK (pista rápida da família HF)

| SAK (hex) | Família provável | UID típico |
|---|---|---|
| 00 | Ultralight / NTAG (memória simples) | 7 bytes |
| 08 | MIFARE Classic 1K | 4 ou 7 bytes |
| 18 | MIFARE Classic 4K | 4 ou 7 bytes |
| 20 | Cripto forte (DESFire e afins) | 7 bytes |

O SAK é pista, não laudo. Cruze com ATQA, tamanho de UID e comportamento. Ver
[cap. 04](04-alta-frequencia-hf.md).

## Variantes do MIFARE Classic

| Variante | SAK | Setores | Blocos | Tamanho |
|---|---|---|---|---|
| Classic Mini | 09 | 5 | 20 | 320 B |
| Classic 1K | 08 | 16 | 64 | 1.024 B |
| Classic 4K | 18 | 40 | 256 | 4.096 B |

Para copiar, o destino tem que ser da mesma variante da origem. Ver
[cap. 05](05-mifare-classic.md).

## Tamanho do UID

| Origem | Destino que casa |
|---|---|
| UID de 4 bytes | destino de 4 bytes |
| UID de 7 bytes | destino de 7 bytes |

Misturar 4 e 7 bytes dá erro de tamanho de UID, porque o layout do bloco 0 é
diferente. Ver [cap. 04](04-alta-frequencia-hf.md).

## Layout do bloco 0 (Classic 1K, UID de 4 bytes)

```
CA CD F5 52 | A0 | 08 | 04 00 | 04 7B 51 AE E3 76 AC 90
UID (4)       BCC  SAK  ATQA     dados de fabricante (8)
```

BCC = XOR dos bytes do UID. Para CA CD F5 52, dá A0.

## Trailer de setor

```
FF FF FF FF FF FF | FF 07 80 69 | FF FF FF FF FF FF
Chave A (6)         access (4)    Chave B (6)
```

FF FF FF FF FF FF com access FF 07 80 69 é o padrão de fábrica. Nunca zere o
trailer com tudo 00, porque access bits inválidos travam o setor.

## Chips LF comuns

| Chip | Ler ID | Reescrever ID | Observação |
|---|---|---|---|
| EM4100 | sim | não | ID fixo de fábrica |
| T5577 | sim | sim | tag em branco, emula outros LF |
| Prox / Indala | sim (o número) | depende | tem facility code e formato |

Copiar ID de LF exige um destino regravável. Ver [cap. 03](03-baixa-frequencia-lf.md).

## Gerações de cartão Magic

| Geração | Como libera o bloco 0 | Risco |
|---|---|---|
| 1 (backdoor) | comandos especiais, sem chave | baixo, regrava sempre |
| 2 (escrita direta) | autenticação normal no bloco 0 | subtipo grava-uma-vez pode travar |
| avançadas | configuráveis por comando (UID, ATQA, SAK) | depende do modelo |

Para aprender e testar, prefira Geração 1. Ver [cap. 06](06-cartoes-magic.md).

## As seis regras práticas

1. Se não ler em HF, teste LF antes de desistir.
2. "Não leu" quase sempre é posição. Varie o lugar sobre a antena.
3. Copiar um ID de LF exige um destino regravável.
4. O tamanho do UID (4 ou 7 bytes) do destino tem que casar com o da origem.
5. Dump com tudo em 00 e chaves FF é sistema UID-only.
6. Depois de gravar, releia o destino e confira.

Voltar ao [índice (README)](../README.md).
