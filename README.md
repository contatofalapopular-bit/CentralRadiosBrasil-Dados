# CentralRadiosBrasil-Dados

Repositório central de dados da Central Rádios Brasil.

## Arquivos

- `radios.json`: cadastro completo usado pelo PWA e pelo painel administrativo.
- `radios-esp32.json`: versão compacta destinada ao firmware ESP32.
- `categorias.json`: categorias oficiais.
- `estados.json`: estados e regiões do Brasil.
- `municipios.json`: municípios cadastrados.
- `versao.json`: versão e nomes dos arquivos publicados.
- `radio.schema.json`: validação básica de uma rádio.

## Regra principal

O painel administrativo deve editar o cadastro completo em `radios.json`.
Depois, uma rotina de publicação deve gerar automaticamente `radios-esp32.json`.

O firmware nunca deve depender dos campos editoriais pesados, como programação,
redes sociais, notícias e histórico de auditoria.

## Identificador

Use IDs estáveis no formato:

`br-uf-cidade-nome-da-radio`

Exemplo:

`br-go-rio-verde-radio-fala-popular`

## Streams

Cada rádio pode ter vários streams. A prioridade menor é tentada primeiro.

- prioridade 1: principal
- prioridade 2: reserva
- prioridade 3: segunda reserva

## Status de monitoramento

Valores recomendados:

- `online`
- `instavel`
- `offline`
- `nao_testado`
- `incompativel`

## Publicação no GitHub

Os arquivos podem ser publicados por GitHub Pages ou acessados pelo endereço RAW.
