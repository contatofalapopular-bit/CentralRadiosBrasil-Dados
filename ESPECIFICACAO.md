# Especificação Oficial Central Rádios Brasil — v1.0

## 1. Objetivo

Este documento define o padrão de cadastro de emissoras utilizado pelo ecossistema
Central Rádios Brasil: Painel Administrativo, PWA, API futura e firmware ESP32.

## 2. Princípios

1. Um único identificador por rádio.
2. Separação entre dados editoriais e dados técnicos.
3. Suporte a vários streams por prioridade.
4. Compatibilidade explícita por plataforma.
5. Histórico e auditoria obrigatórios.
6. Validação automática sempre que possível.
7. O firmware ESP32 recebe apenas uma versão compacta dos dados.

## 3. Identificador oficial

Formato recomendado:

`br-uf-cidade-nome-da-radio`

Exemplo:

`br-go-rio-verde-radio-fala-popular`

Regras:
- letras minúsculas;
- sem acentos;
- palavras separadas por hífen;
- não deve mudar depois de publicado;
- deve ser único em todo o banco.

## 4. Campos obrigatórios

- `id`
- `nome`
- `slug`
- `tipo`
- `ativa`
- `verificada`
- `idioma`
- `localizacao`
- `categoriaPrincipal`
- `categorias`
- `streams`
- `statusCadastro`
- `auditoria`

## 5. Streams

Cada rádio pode possuir até cinco streams.

Prioridades:
- `1`: principal;
- `2`: primeira reserva;
- `3`: segunda reserva;
- `4` e `5`: reservas adicionais.

O consumidor deve tentar os streams ativos em ordem crescente de prioridade.

## 6. Estados de monitoramento

- `online`
- `instavel`
- `offline`
- `nao_testado`
- `incompativel`

## 7. Estados do cadastro

- `rascunho`
- `enviado`
- `em_validacao`
- `correcao_solicitada`
- `aprovado`
- `publicado`
- `suspenso`
- `arquivado`

## 8. Compatibilidade

Cada stream deve indicar separadamente:
- navegador;
- Android;
- iOS;
- ESP32.

O valor pode ser:
- `true`: testado e compatível;
- `false`: testado e incompatível;
- `null`: ainda não testado.

## 9. Programação

Os horários usam o formato `HH:MM`, em 24 horas.
O fuso horário deve usar o padrão IANA, por exemplo:

`America/Sao_Paulo`

Dias aceitos:
- segunda
- terca
- quarta
- quinta
- sexta
- sabado
- domingo

## 10. Arquivos do ecossistema

- `radios.json`: cadastro completo;
- `radios-esp32.json`: versão compacta;
- `categorias.json`: categorias oficiais;
- `estados.json`: estados e regiões;
- `municipios.json`: municípios;
- `versao.json`: versão do conjunto;
- `radio.schema.json`: validação formal.

## 11. Regra de publicação

O Painel Administrativo nunca deve editar diretamente `radios-esp32.json`.

Fluxo correto:

`Painel → radios.json → validador → gerador → radios-esp32.json → publicação`

## 12. Versão

Esta especificação é a versão `1.0.0`.

Alterações incompatíveis devem aumentar a versão principal.
Campos opcionais novos podem aumentar a versão secundária.
Correções de documentação podem aumentar a versão de revisão.
