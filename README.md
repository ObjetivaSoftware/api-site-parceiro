
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

Para consumir a API, é necessário obter um <strong>ClientID</strong> e um <strong>SecretID</strong> junto à Imobiliária. Solicite suas credenciais no painel de Chaves de API do <b>Gestor Imobiliária</b>.

### 1. Obtenha seu ClientID e SecretID
Entre em contato com a Imobiliária para receber suas credenciais de acesso.

### 2. Gere o Access Token
Faça uma requisição <b>POST</b> para o endpoint:

```
POST /access-token
```

#### Exemplo de Requisição
```json
{
	"clientID": "ab4432e6-1f5d-4a06-b4c5-09893c374b16",
	"secretID": "59882a7c-7774-4eb7-b5a0-87d1f70e68c6"
}
```

#### Exemplo de Resposta
```json
{
	"access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
	"token_type": "Bearer",
	"expires_in": 1757443191
}
```

### 3. Use o Access Token
Inclua o token no header <code>Authorization</code> de todas as requisições:

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
- **Descrição:** Retorna a lista de imóveis públicos disponíveis.
- **Headers:**
	- Authorization: Bearer {access_token}

#### Exemplo de Requisição
```bash
curl -X GET \
	-H "Authorization: Bearer {access_token}" \
	"https://api-site-parceiro.gestorimob.com.br/imoveis"
```

---

### Detalhes de um Imóvel

- **Endpoint:**
	```
	GET /imovel/{id}
	```
- **Descrição:** Retorna informações detalhadas de um imóvel específico.
- **Headers:**
	- Authorization: Bearer {access_token}
- **Parâmetros:**
	- <code>id</code>: ID do imóvel desejado

#### Exemplo de Requisição
```bash
curl -X GET \
	-H "Authorization: Bearer {access_token}" \
	"https://api-site-parceiro.gestorimob.com.br/imovel/xyz"
```

---

## 🚀 Boas Práticas
- Sempre utilize HTTPS para garantir a segurança dos dados.
- O token de acesso possui validade. Solicite um novo token quando necessário.
- Não compartilhe seu ClientID e SecretID publicamente.

---

## 💬 Suporte
Em caso de dúvidas, entre em contato com a Imobiliária responsável ou abra uma issue neste repositório.

---

<div align="center">
	<b>Feito com ❤️ para facilitar sua integração!</b>
</div>
