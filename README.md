# Vejo em casa - Wordpress

## Como usar a API do Eu Pago

### Endpoints
* Demo: https://sandbox.eupago.pt/clientes/rest_api (API KEY para demo: `demo-cf0c-36f8-4ef2-625`)
* Prod: https://clientes.eupago.pt/clientes/rest_api

Mais info: https://suporte.eupago.pt/pt/article/261-rest-api

### Flow:
![](https://www.websequencediagrams.com/cgi-bin/cdraw?lz=cGFydGljaXBhbnQgRnJvbnRlbmQgYXMgRgoADgxCYWNrABIHQgAMDUV1IFBhZ28gYXMgRVAKCm5vdGUgbGVmdCBvZiBGOiBVdGlsaXphZG9yIGFicmUgYSBww6FnaW5hIGRvIHZpZGVvCkYgLT4gQjogUGVkaXIgaW5mb3JtYcOnw7VlcyBkbyBldmVudG8gZSBkbyBjcmkARgXDoCBEQgpCIC0-IEY6IEkAECMAYAZGOiBFeHRyYWlyIEFQSSBLRVkASgxuYSByZXNwb3N0YQAmCQCBNQtjYXJyZWdhIG5vIGJvdMOjbyBwYXJhIGVmZWN0dWFyIGRvbmF0aXZvCgphbHQgTUJXYXkKICAgIAByCE1vc3RyYXIgZm9ybQA1Bm8gdQCCFQpcbmluc2VyaXIgbyBzZXUgbsO6bWVybyBkZSB0ZWxlZm9uZSBlIFxuYSBxdWFudGlkYWRlIGRlIOKCrCBxdWUgcHJldGVuZGUgZW52aWFyAHEKRVA6IENoYW1hAIFvBi9tYndheS9jcmVhdGUAgRwFRVAAgkIHMjAwIE9LAIEoDQCCVQdyAIEeDmRldmUgXG5jb25jbHUAgS0FcGFnYW1lbnRvXG5uYSBhcGxpY2HDp8OjbwCBfgsAhAEbcmVjZWJlIG5vdGlmADEJbm8AgXUFbcOzdmVsLgplbHNlIE11bHRpYmFuY28AgjAsAIJSCACBekQAeAkAgi4VRGFkbwCFMgUAgggJIAAoCgCDehVkACASKEUAg1kHLCByZWZlcmVuY2lhLCB2YWxvcikAgisgAIUJBwCDCAxodHRwczovL3d3dy53ZWJzZXF1ZW5jZWRpYWdyYW1zLmNvbS8_cG5nPW1zYzIxMTkxNjE1NyBwAIMTBWZlcsOqbmNpYQCBPAxlbmQKCg&s=magazine)


### MBWay
#### Pedido (POST):
```
{
    "chave": "demo-cf0c-36f8-4ef2-625",
    "valor": 1.00,
    "id": "video_1_bruno_nogueira",
    "alias": "910000000",
    "descricao": "Optional"
}
```
* `chave`: A API KEY de cada criador
* `valor`: Valor que o utilizador introduziu que pretende enviar
* `id`: Valor escolhido por nós. Útil para no Eu Pago se conseguir identificar qual a fonte de rendimento. Sugestão: identificador do video e do criador
* `alias`: Número de MBWay que o utilizador introduziu
* `descrição`: Opcional

#### Resposta:
```
{
    "sucesso": true,
    "estado": 0,
    "resposta": "OK",
    "referencia": 8813461,
    "valor": "1.00000",
    "alias": "351#910000000"
}
```
* Neste caso penso que basta olha para o status code e para o campo `sucesso`

### Multibanco
#### Pedido (POST):
```
{
    "chave": "demo-cf0c-36f8-4ef2-625",
    "valor": 5.00,
    "id": "video_23_jose_avillez",
    "per_dup": true
}
```
* `chave`: A API KEY de cada criador
* `valor`: Valor que o utilizador introduziu que pretende enviar
* `id`: Valor escolhido por nós. Útil para no Eu Pago se conseguir identificar qual a fonte de rendimento. Sugestão: identificador do video e do criador
* `per_dup`: Indicação se a mesma referência pode ser utilizada várias vezes. Neste caso, enviar sempre a `true`

#### Resposta:
```
{
    "sucesso": true,
    "estado": 0,
    "resposta": "OK",
    "referencia": "302354681",
    "valor": "5.00000",
    "entidade": "82229"
}
```
Neste caso tem que se olha para o status code e para o campo `sucesso` vara validar se o pedido foi feito correctamente.

De seguida, os valores `entidade`, `referencia` e `valor` devem ser apresentados ao utilizador
