# 🔗 API Integrations — REST · OAuth 2.0 · Monitoramento

> Exemplos práticos e padrões reutilizáveis de integração com APIs REST, desenvolvidos a partir de experiência real em ambientes de telecomunicações, ERP e cloud.

---

## 🧠 Por que este repositório existe

Ao longo de anos trabalhando com integração entre APIs, ERPs, aplicações web e serviços em nuvem, aprendi na prática o que funciona e o que quebra em produção. Este repositório consolida esses padrões de forma reutilizável.

---

## 📂 Estrutura

```
api-integrations/
├── 📁 auth/
│   ├── oauth2_client_credentials.py   # Fluxo Client Credentials
│   ├── oauth2_refresh_token.py        # Fluxo com Refresh Token
│   └── token_cache.py                 # Cache + renovação automática
│
├── 📁 patterns/
│   ├── retry_with_backoff.py          # Retry exponencial com jitter
│   ├── circuit_breaker.py             # Circuit breaker simples
│   ├── payload_validator.py           # Validação de schema (JSONSchema)
│   └── response_normalizer.py        # Normalização de respostas entre sistemas
│
├── 📁 monitoring/
│   ├── health_checker.py              # Verificação de saúde de endpoints
│   ├── contract_tester.py             # Testes de contrato de API
│   └── alert_sender.py               # Envio de alertas (webhook/e-mail)
│
├── 📁 examples/
│   ├── operacoes-digitais/              # Padrões para integrações críticas
│   ├── erp_sap/                       # Integração com sistemas ERP
│   └── cloud_aws/                     # Integrações com serviços AWS
│
└── 📁 postman/
    └── collections/                   # Collections Postman exportadas
```

---

## 🔑 Autenticação OAuth 2.0

O padrão mais crítico em ambientes corporativos. Implementação completa do fluxo Client Credentials com cache e renovação automática:

```python
from auth.oauth2_client_credentials import OAuthClient

client = OAuthClient(
    token_url="https://auth.sistema.com/oauth/token",
    client_id="seu_client_id",
    client_secret="seu_client_secret",
    scope="api.read api.write"
)

# Token renovado automaticamente antes de expirar
headers = client.get_auth_headers()
```

---

## 🔁 Retry com Backoff Exponencial

Essencial para integrações em produção — evita cascata de falhas em momentos de instabilidade:

```python
from patterns.retry_with_backoff import retry

@retry(max_attempts=3, base_delay=1.0, max_delay=30.0, jitter=True)
def chamar_api_externa(payload):
    response = requests.post(url, json=payload, headers=headers)
    response.raise_for_status()
    return response.json()
```

---

## 📋 Validação de Payload

Garante que contratos de API sejam respeitados — identifica quebras de contrato antes que causem incidentes:

```python
from patterns.payload_validator import validate_payload

schema = {
    "type": "object",
    "required": ["customerId", "status", "processingWindow"],
    "properties": {
        "customerId": {"type": "string"},
        "status": {"type": "string", "enum": ["ACTIVE", "SUSPENDED", "CANCELLED"]},
        "processingWindow": {"type": "integer", "minimum": 1}
    }
}

resultado = validate_payload(response_data, schema)
```

---

## 📡 Monitoramento de Contratos

Testa continuamente se as APIs retornam o que prometem:

```bash
# Configura as APIs a monitorar
cp config/apis.example.yaml config/apis.yaml

# Roda o monitor (verifica a cada 5 minutos)
python monitoring/contract_tester.py --interval 300

# Resultado
✅  POST /api/consulta        → 200 OK  · 342ms · Schema válido
✅  GET  /api/status/{customerId} → 200 OK  · 178ms · Schema válido
⚠️  GET  /api/processing-window  → 200 OK  · 2341ms · LENTO (threshold: 1000ms)
❌  POST /api/provisioning     → 503     · Sistema indisponível
```

---

## 🛠️ Stack

```
Python 3.10+
Requests / HTTPX
JSONSchema (jsonschema)
Pydantic (validação de modelos)
Pytest (testes de contrato)
PyYAML (configuração)
```

---

## 🚀 Início rápido

```bash
git clone https://github.com/SEU_USUARIO/api-integrations.git
cd api-integrations

python -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# Rode os exemplos
python examples/telecomunicacoes/consulta_basica.py

# Rode os testes
pytest tests/ -v
```

---

## 📬 Coleções Postman

A pasta `postman/collections/` contém collections exportadas com:
- Exemplos de autenticação OAuth 2.0
- Requests de consulta e aprovisionamento
- Testes automatizados de contrato
- Variáveis de ambiente por sistema

Importe diretamente no Postman: `File → Import → selecione o arquivo .json`

---

## 💡 Lições aprendidas em produção

- **Sempre valide o payload antes de processar** — sistemas legados mudam contratos sem avisar
- **Cache de tokens é obrigatório** — uma nova requisição de token por chamada quebra o rate limit
- **Retry sem jitter cria thundering herd** — adicione aleatoriedade ao delay
- **Log o `transaction_id`** — sem ele, RCA em ambiente distribuído é impossível
- **Monitore tempo de resposta, não só status** — 200 lento é pior que 503 rápido em SLA

---

## 👤 Autor

**Gustavo Miranda**  
Especialista em Automação e IA Aplicada | Integração de Sistemas<br>
📍 São Bernardo do Campo, SP — Remoto  
🔗 [LinkedIn](https://www.linkedin.com/in/gustavo-miranda-84178bb5/)
