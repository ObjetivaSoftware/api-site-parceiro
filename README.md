
<div align="center">
  <img src="https://img.shields.io/badge/API-RESTful-blue" alt="API RESTful" />
  <h1>API Site Parceiro - Documentação Oficial</h1>
  <p>Integre facilmente com a API do Gestor Imobiliária para acessar dados de imóveis públicos.</p>
</div>

---

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
        "codigo": "14786",
        "tipo": {
          "codigo": "4",
          "nome": "Apartamento",
          "descricao": "Apartamentos",
          "acaoCodigo": "2"
        },
        "acao": {
          "codigo": "2",
          "nome": "Vende-se",
          "descricao": "Vende-se imóveis"
        },
        "valor": 500000,
        "valorFormatado": "500.000,00",
        "descricao": "Vende-se aparatmento com linda vista ara cidade - Próximo a escola",
        "enderecoCompleto": "Rua Felicio, 10, Ap 801, Centro, Marau/Rio Grande do Sul, 99150-000",
        "linkImagemPrincipal": "https://img.sis.gestorimob.com.br/1/imoveis/thumb/741921764852918759.webp",
        "detalhes": []
      }
    ],
    "_links": {
      "self": {
        "href": "http://localhost:8080/imoveis?page=1&per_page=10",
        "title": "Listagem de imóveis - página 1",
        "type": "application/json"
      },
      "next": {
        "href": "http://localhost:8080/imoveis?page=2&per_page=10",
        "title": "Próxima página",
        "type": "application/json"
      },
      "prev": null
    }
  },
  "meta": {
    "timestamp": "2025-09-10T16:41:35Z",
    "total": 28,
    "page": 1,
    "per_page": 10,
    "total_pages": 3
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
      "codigo": "14804",
      "tipo": {
        "codigo": "25",
        "nome": "Cobertura Duplex",
        "descricao": "Cobertura Duplex"
      },
      "acao": {
        "codigo": "3",
        "nome": "Lançamento",
        "descricao": "Lançamentos"
      },
      "uso": "Residencial",
      "status": "Imóvel novo",
      "MCMV": false,
      "valor": 2500000,
      "valorFormatado": "2.500.000,00",
      "titulo": "Vende-se cobertura",
      "descricao": "<p>Magnífica cobertura duplex com vista panorâmica da cidade! Este exclusivo imóvel oferece sofisticação e conforto em cada detalhe, proporcionando uma experiência de moradia única em localização privilegiada no coração de Marau. Ideal para quem busca requinte e qualidade de vida excepcional.</p>",
      "publicarNoSite": true,
      "proprietarios": [
        {
          "codigo": 11,
          "nome": "Madalena Regina Beria",
          "documento": "287.904.730-78"
        }
      ],
      "corretor": {
        "nome": "Madalena Regina"
      },
      "linkImagemPrincipal": "https://img.sis.gestorimob.com.br/1/imoveis/thumb/403814699600554120.webp",
      "localizacao": {
        "cep": "99150-000",
        "logradouro": "Av. Pres. Vargas",
        "numero": "521",
        "complemento": "Ap. 1002",
        "bairro": "Centro",
        "cidade": "Marau",
        "estado": "RS",
        "latitude": "-28.4497540",
        "longitude": "-52.1986250",
        "enderecoCompleto": "Av. Pres. Vargas, 521, Ap. 1002, Centro, Marau/RS, 99150-000"
      },
      "detalhes": {
        "tags": "Cobertura, Apartamento Duplex",
        "codigoInterno": "955959",
        "matricula": "2559559",
        "informacoes": "Informações internas"
      },
      "imagens": [
        {
          "ordem": 0,
          "link": "https://img.sis.gestorimob.com.br/1/imoveis/403814699600554120.webp",
          "legenda": ""
        },
        {
          "ordem": 1,
          "link": "https://img.sis.gestorimob.com.br/1/imoveis/122445860697528448.webp",
          "legenda": ""
        },
        {
          "ordem": 2,
          "link": "https://img.sis.gestorimob.com.br/1/imoveis/595276296901460888.webp",
          "legenda": ""
        },
        {
          "ordem": 3,
          "link": "https://img.sis.gestorimob.com.br/1/imoveis/347369501971460828.webp",
          "legenda": ""
        }
      ],
      "comodos": {
        "sala": 2,
        "quarto": 3,
        "banheiro": 1,
        "suite": 2,
        "demisuite": 1,
        "areaservico": 1,
        "vaga": 2,
        "lavabo": 2,
        "cozinha": 1,
        "sacada": 1
      },
      "areas": {
        "total": "0.00",
        "privativa": "200.00",
        "lote": "0.00"
      },
      "IPTU": {
        "valor": "1500.00",
        "tipoCobranca": "Total",
        "observacoes": ""
      },
      "seguroIncendio": {
        "ativo": true,
        "valor": "100",
        "tipoCobranca": "Mensal",
        "observacoes": ""
      },
      "seguroFianca": {
        "ativo": true,
        "valor": "100.00",
        "tipoCobranca": "Total",
        "observacoes": ""
      },
      "infraestruturas": [
        {
          "grupo": "Acabamentos",
          "itens": ["Piso de pedra", "Esquadrias em  PVC"]
        },
        {
          "grupo": "Apartamento",
          "itens": ["Mobiliado", "Dependência de empregada", "Escritório"]
        }
      ]
    },
    "_links": {
      "self": {
        "href": "http://localhost:8080/imovel?id=14786",
        "title": "Informação do imóvel",
        "type": "application/json"
      }
    }
  },
  "meta": {
    "timestamp": "2025-09-10T16:41:55Z"
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
