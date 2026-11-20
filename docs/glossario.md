# Glossário

Termos que aparecem ao longo do guia, reunidos em um lugar só. Serve para quem
cai direto num capítulo do meio e esbarra numa sigla.

## Frequência e física

**RFID (Radio-Frequency Identification)**
Conjunto de tecnologias em que uma credencial troca dados com um leitor por ondas
de rádio, sem contato.

**NFC (Near Field Communication)**
Um subconjunto do HF (13,56 MHz) voltado a curtíssimo alcance. É o que o celular
usa para ler tags.

**LF (baixa frequência)**
Faixa em torno de 125 kHz (às vezes 134 kHz). Dados simples, quase sempre só um
ID. Ver [capítulo 03](03-baixa-frequencia-lf.md).

**HF (alta frequência)**
Faixa de 13,56 MHz. Memória estruturada e, em muitos chips, criptografia. Ver
[capítulo 04](04-alta-frequencia-hf.md).

**Acoplamento indutivo**
Jeito como a credencial passiva recebe energia: a bobina do leitor gera um campo
magnético que induz tensão na bobina da credencial. Mesma ideia de um
transformador sem fio.

**Modulação de carga**
Forma como a credencial responde. Ela não gera sinal próprio, varia a própria
carga (liga e desliga uma resistência) e o leitor detecta essa variação no campo.

**Ressonância / capacitor de sintonia**
A bobina mais um capacitor formam um circuito afinado na frequência de operação.
Sintonia ruim reduz o alcance.

## Credencial e leitor

**Credencial**
Termo geral para o objeto que carrega o chip: cartão, tag, chaveiro, adesivo,
pulseira, token.

**Tag**
Uma credencial RFID. Neste guia, costuma indicar os formatos que não são cartão
(chaveiro, token, adesivo), mas o uso é solto.

**Passiva**
Sem bateria própria. É energizada pelo campo do leitor. A maioria das credenciais
de proximidade é passiva.

**Leitor**
O lado ativo, com energia. Gera o campo e comanda a conversa.

**Emulador**
Dispositivo que finge ser uma tag. Ler um emulador com outro leitor é menos
confiável que ler uma tag física passiva.

## Memória e silício

**ROM**
Memória só de leitura, gravada de fábrica. Nenhuma ferramenta reescreve.

**EEPROM**
Memória regravável. Pode ou não aceitar escrita, conforme os bits de bloqueio.

**Bloco**
Unidade de memória do MIFARE Classic, de 16 bytes.

**Setor**
Grupo de blocos no Classic. No 1K são 16 setores de 4 blocos cada.

**Trailer de setor**
O último bloco de cada setor. Guarda Chave A, access bits e Chave B.

**Bloco 0 (fabricante)**
Primeiro bloco do setor 0. Guarda UID, BCC, SAK e ATQA. Travado de fábrica num
cartão comum.

## Identidade (ISO 14443-A)

**UID (Unique Identifier)**
Número de série da tag. Tem 4 bytes (curto) ou 7 bytes (longo). O tamanho decide
compatibilidade de cópia.

**ATQA (Answer To reQuest, type A)**
2 bytes que a tag envia ao ser chamada. Dá dicas do tipo e do tamanho do UID.

**SAK (Select AcKnowledge)**
1 byte enviado ao final da seleção. É a pista rápida da família do chip (00 NTAG,
08 Classic 1K, 18 Classic 4K, 20 cripto forte).

**BCC**
Byte de verificação do bloco 0, igual ao XOR dos bytes do UID. Se não bate, a
seleção falha. Para o UID CA CD F5 52, o BCC é A0.

**Access bits**
4 bytes no trailer que definem o que cada chave pode fazer em cada bloco. Valor
inválido trava o setor.

**Chave A / Chave B**
As duas senhas de 6 bytes de cada setor. Para ler ou escrever um setor é preciso
autenticar com uma delas. O padrão de fábrica é FF FF FF FF FF FF.

## Tipos e famílias

**EM4100**
Família LF só de leitura, ID de 40 bits fixo de fábrica. Comum em acesso legado.

**T5577**
Transponder LF regravável. Serve de tag em branco e consegue emular outros
protocolos LF, inclusive EM4100.

**Prox / Indala**
Formatos de acesso LF que carregam, além do número, um código de instalação
(facility) e um formato de bits.

**Ultralight / NTAG**
Família HF de memória simples (SAK em geral 00, UID de 7 bytes). Não guarda um
dump de Classic.

**MIFARE Classic**
Chip HF com setores e chaves. 1K (SAK 08) ou 4K (SAK 18). O alvo mais comum em
controle de acesso.

**DESFire**
Chip HF com criptografia forte (SAK tipo 20). Na prática não é clonável como um
Classic.

**Cartão Magic**
Credencial HF em branco cujo bloco 0 é gravável, ou seja, dá para mudar o UID.
Existe para permitir cópia. Ver [capítulo 06](06-cartoes-magic.md).

**UID-only**
Sistema de acesso que só confere o UID e ignora o conteúdo dos setores. Num dump,
aparece como dados todos 00 e chaves todas FF.

**Wiegand**
Formato de bits usado em controle de acesso para empacotar o número do cartão e o
facility code.

Voltar ao [índice (README)](../README.md).
