
<div align="center">
  <img src="https://img.shields.io/badge/API-RESTful-blue" alt="API RESTful" />
  <h1>API Site Parceiro - Documentação Oficial</h1>
  <p>Integre facilmente com a API do Gestor Imobiliária para acessar dados de imóveis públicos.</p>
</div>

---

## Live Demo
https://objetivasoftware.github.io/api-site-parceiro/

## 🌐 Base URL

```
https://api-site-parceiro.gestorimob.com.br
```

## 🔒 Autenticação

Para consumir a API, é necessário obter um **ClientID** e um **SecretID** junto à Imobiliária. Solicite suas credenciais no painel de Chaves de API do **Gestor Imobiliária**.

### 1. Obtenha seu ClientID e SecretID
Entre em contato com a Imobiliária para receber suas credenciais de acesso.

### 2. Gere o Access Token
Faça uma requisição **POST** para o endpoint:

```
POST /accesstoken
```

#### Exemplo de Requisição
```bash
curl --request POST \
  --url https://api-site-parceiro.gestorimob.com.br/accesstoken \
  --data '{
    "clientID":"ab4432e6-1f5d-4a06-b4c5-09893c374b16",
    "secretID":"59882a7c-7774-4eb7-b5a0-87d1f70e68c6"
  }'
```

#### Exemplo de Resposta
```json
{
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJhcGktc2l0ZS1wYXJjZWlybyIsImF1ZCI6ImFwaS1zaXRlLXBhcmNlaXJvIiwiaWF0IjoxNzU3NTIyNDc4LCJuYmYiOjE3NTc1MjI0NzgsImV4cCI6MTc1NzUyMjc3OCwiY2xpZW50SUQiOiJhYjQ0MzJlNi0xZjVkLTRhMDYtYjRjNS0wOTg5M2MzNzRiMTYifQ.Z_2dovre-7GkVFTRtsW72h-zZv3xKVkLE7QMgaJQapU",
  "token_type": "Bearer",
  "expires_in": 1757522778
}
```

### 3. Use o Access Token
Inclua o token no header `Authorization` de todas as requisições:

```
Authorization: Bearer {access_token}
```

---

## 📚 Endpoints Principais

### Listar Imóveis Públicos

- **Endpoint:**
  ```
  GET /imoveis
  ```
- **Descrição:** Retorna a lista de imóveis públicos disponíveis com paginação.
- **Headers:**
  - Authorization: Bearer {access_token}
  - Content-Type: application/json
- **Parâmetros Opcionais:**
  - `page`: Número da página (padrão: 1)
  - `per_page`: Itens por página (padrão: 10)

#### Exemplo de Requisição
```bash
curl --request GET \
  --url "https://api-site-parceiro.gestorimob.com.br/imoveis" \
  --header "Authorization: Bearer {access_token}" \
  --header "Content-Type: application/json"
```

#### Exemplo de Resposta
```json
{
  "status": "success",
  "data": {
    "imoveis": [
      {
        "codigo": "1307",
        "status": "Em construção",
        "comodos": {
          "sala": 0,
          "quarto": 1,
          "banheiro": 1,
          "suite": 0,
          "demisuite": 0,
          "areaservico": 0,
          "vaga": 0,
          "lavabo": 0,
          "cozinha": 0,
          "sacada": 0
        },
        "areas": {
          "total": "0.00",
          "privativa": "67.65",
          "lote": "0.00"
        },
        "tipo": {
          "codigo": "20",
          "nome": "Cobertura Duplex",
          "descricao": "Cobertura Duplexs",
          "acaoCodigo": "3"
        },
        "acao": {
          "codigo": "3",
          "nome": "Lançamento",
          "descricao": "Lançamentos"
        },
        "valor": 325600,
        "endereco": {
          "cep": "01507-001",
          "logradouro": "Rua Barão de Iguape, 855",
          "numero": "855",
          "complemento": "",
          "bairro": "Liberdade",
          "cidade": "São Paulo",
          "estado": "SP",
          "latitude": -23.557998,
          "longitude": -46.62864
        },
        "valorFormatado": "325.600,00",
        "descricao": "Empreendimento Residencial em Liberdade São Paulo - SP",
        "enderecoCompleto": "Rua Barão de Iguape, 855, 855, Liberdade, São Paulo/São Paulo, 01507-001",
        "linkImagemPrincipal": "https://img.sis.gestorimob.com.br/461/imoveis/thumb/external-1630700-79339_51802-1630700.jpg"
      }
    ],
    "_links": {
      "self": {
        "href": "https://api-site-parceiro.gestorimob.com.br/imoveis?page=1&per_page=1",
        "title": "Listagem de imóveis - página 1",
        "type": "application/json"
      },
      "next": {
        "href": "https://api-site-parceiro.gestorimob.com.br/imoveis?page=2&per_page=1",
        "title": "Próxima página",
        "type": "application/json"
      },
      "prev": null
    }
  },
  "meta": {
    "timestamp": "2025-09-26T17:07:12Z",
    "total": 1997,
    "page": 1,
    "per_page": 1,
    "total_pages": 1997
  }
}
```

---

### Detalhes de um Imóvel

- **Endpoint:**
  ```
  GET /imoveis?id={id}
  ```
- **Descrição:** Retorna informações detalhadas de um imóvel específico, incluindo todas as imagens.
- **Headers:**
  - Authorization: Bearer {access_token}
  - Content-Type: application/json
- **Parâmetros:**
  - `id`: ID do imóvel desejado (obrigatório)

#### Exemplo de Requisição
```bash
curl --request GET \
  --url "https://api-site-parceiro.gestorimob.com.br/imoveis?id=14786" \
  --header "Authorization: Bearer {access_token}" \
  --header "Content-Type: application/json"
```

#### Exemplo de Resposta

```json
{
  "status": "success",
  "data": {
    "imovel": {
      "codigo": "1307",
      "tipo": {
        "codigo": "20",
        "nome": "Cobertura Duplex",
        "descricao": "Cobertura Duplexs"
      },
      "acao": {
        "codigo": "3",
        "nome": "Lançamento",
        "descricao": "Lançamentos"
      },
      "uso": "Residencial",
      "status": "Em construção",
      "MCMV": false,
      "valor": 325600,
      "valorFormatado": "325.600,00",
      "titulo": "Empreendimento Residencial em Liberdade São Paulo - SP",
      "descricao": "Um empreendimento completo com toda segurança, conforto e lazer que você merece. Preço e disponibilidade do imóvel sujeitos a alteração sem aviso prévio.",
      "publicarNoSite": true,
      "proprietarios": [],
      "corretor": {
        "nome": "Julio Barbiellini"
      },
      "linkImagemPrincipal": "https://img.sis.gestorimob.com.br/461/imoveis/thumb/external-1630700-79339_51802-1630700.jpg",
      "localizacao": {
        "cep": "01507-001",
        "logradouro": "Rua Barão de Iguape, 855",
        "numero": "855",
        "complemento": "",
        "bairro": "Liberdade",
        "cidade": "São Paulo",
        "estado": "SP",
        "latitude": "-23.5579980",
        "longitude": "-46.6286400",
        "enderecoCompleto": "Rua Barão de Iguape, 855, 855, Liberdade, São Paulo/SP, 01507-001"
      },
      "detalhes": {
        "tags": "",
        "codigoInterno": "79339_51802",
        "matricula": "",
        "informacoes": "Referência: 11502 \nAtualizado em: 18/09/2025 07:17:18"
      },
      "imagens": [
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630700-79339_51802-1630700.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630701-79339_51802-1630701.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630702-79339_51802-1630702.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630703-79339_51802-1630703.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630704-79339_51802-1630704.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630705-79339_51802-1630705.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630706-79339_51802-1630706.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630707-79339_51802-1630707.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630708-79339_51802-1630708.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630709-79339_51802-1630709.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630710-79339_51802-1630710.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630711-79339_51802-1630711.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630712-79339_51802-1630712.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630713-79339_51802-1630713.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630714-79339_51802-1630714.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630715-79339_51802-1630715.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630716-79339_51802-1630716.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630717-79339_51802-1630717.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630718-79339_51802-1630718.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630719-79339_51802-1630719.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630720-79339_51802-1630720.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630721-79339_51802-1630721.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630722-79339_51802-1630722.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630723-79339_51802-1630723.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630724-79339_51802-1630724.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630725-79339_51802-1630725.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630726-79339_51802-1630726.jpg",
          "legenda": ""
        },
        {
          "ordem": 5000,
          "link": "https://img.sis.gestorimob.com.br/461/imoveis/external-1630727-79339_51802-1630727.jpg",
          "legenda": ""
        }
      ],
      "comodos": {
        "sala": 0,
        "quarto": 1,
        "banheiro": 1,
        "suite": 0,
        "demisuite": 0,
        "areaservico": 0,
        "vaga": 0,
        "lavabo": 0,
        "cozinha": 0,
        "sacada": 0
      },
      "areas": {
        "total": "0.00",
        "privativa": "67.65",
        "lote": "0.00"
      },
      "IPTU": {
        "valor": 0,
        "tipoCobranca": "Mensal",
        "observacoes": ""
      },
      "seguroIncendio": {
        "ativo": false,
        "valor": 0,
        "tipoCobranca": "Mensal",
        "observacoes": ""
      },
      "seguroFianca": {
        "ativo": false,
        "valor": 0,
        "tipoCobranca": "Total",
        "observacoes": ""
      },
      "infraestruturas": []
    },
    "_links": {
      "self": {
        "href": "https://api-site-parceiro.gestorimob.com.br/imovel?id=1307",
        "title": "Informação do imóvel",
        "type": "application/json"
      },
      "update": {
        "href": "https://api-site-parceiro.gestorimob.com.br/imovel?id=1307",
        "title": "Atualizar informação do imóvel",
        "type": "application/json"
      },
      "delete": {
        "href": "https://api-site-parceiro.gestorimob.com.br/imovel?id=1307",
        "title": "Deletar o imóvel",
        "type": "application/json"
      }
    }
  },
  "meta": {
    "timestamp": "2025-09-26T17:09:05Z"
  }
}
```

---

## 🚀 Boas Práticas
- Sempre utilize HTTPS para garantir a segurança dos dados.
- O token de acesso possui validade. Solicite um novo token quando necessário.
- Não compartilhe seu ClientID e SecretID publicamente.
- A API retorna respostas paginadas para listagens. Use os parâmetros `page` e `per_page` para navegar pelos resultados.
- Utilize os links na resposta (`_links`) para navegação entre páginas.

---

## 📋 Estrutura de Resposta

### Resposta Padrão
Todas as respostas seguem o padrão:
```json
{
  "status": "success|error",
  "data": {
    // dados específicos do endpoint
  },
  "meta": {
    "timestamp": "2025-09-10T16:41:35Z",
    // metadados adicionais como paginação
  }
}
```

### Paginação
Para endpoints que retornam listas, a resposta inclui:
- `meta.total`: Total de registros
- `meta.page`: Página atual
- `meta.per_page`: Itens por página
- `meta.total_pages`: Total de páginas
- `_links`: Links para navegação (self, next, prev)

---

## 💬 Suporte
Em caso de dúvidas, entre em contato com a Imobiliária responsável ou abra uma issue neste repositório.

---

<div align="center">
  <b>Feito com ❤️ para facilitar sua integração!</b>
</div>
