# 🐍 Automações Python — Operações & Sistemas

> Coleção de scripts e ferramentas de automação desenvolvidos ao longo de mais de 10 anos de atuação em ambientes de alta complexidade — telecomunicações, ERP, cloud e integração de sistemas.

---

## 📂 Categorias

```
automacoes-python/
├── 📁 oauth-token-manager/       # Geração e renovação automática de tokens OAuth 2.0
├── 📁 api-monitor/               # Monitoramento de contratos e saúde de APIs REST
├── 📁 etl-scripts/               # Pipelines ETL para sincronização entre sistemas
├── 📁 log-analyzer/              # Parser e análise de logs para investigação de incidentes (RCA)
├── 📁 report-generator/          # Geração automática de relatórios operacionais
└── 📁 notifications/             # Alertas automáticos via e-mail/webhook
```

---

## 🛠️ Stack principal

```
Linguagem      → Python 3.10+
Web/API        → FastAPI · Requests · HTTPX
Automação      → Playwright · Selenium
Dados          → Pandas · OpenPyXL
Agendamento    → APScheduler · Cron
Logs           → Loguru · Structlog
Testes         → Pytest
```

---

## 🔑 oauth-token-manager

Módulo reutilizável para geração, cache e renovação automática de tokens OAuth 2.0. Desenvolvido originalmente para a operação MVNO Nubank Claro, onde múltiplos sistemas exigiam tokens independentes.

**Funcionalidades:**
- Suporte a múltiplos `client_id / client_secret` simultaneamente
- Cache em memória com renovação automática antes da expiração
- Retry com backoff exponencial em caso de falha
- Log estruturado de cada operação de autenticação

```python
from oauth_manager import TokenManager

manager = TokenManager(
    client_id="seu_client_id",
    client_secret="seu_client_secret",
    token_url="https://auth.sistema.com/oauth/token"
)

token = manager.get_token()  # Renovado automaticamente quando necessário
```

---

## 📡 api-monitor

Script de monitoramento contínuo de APIs REST — verifica disponibilidade, tempo de resposta e conformidade do payload retornado com o contrato esperado.

**Funcionalidades:**
- Verificação de status HTTP e tempo de resposta
- Validação de schema do payload (JSONSchema)
- Alertas automáticos por webhook (Slack, Teams, e-mail)
- Dashboard simples em HTML com histórico de disponibilidade

```bash
python api_monitor.py --config apis.yaml --interval 60
```

---

## 🔄 etl-scripts

Pipelines ETL desenvolvidos para sincronização entre sistemas heterogêneos (Oracle, SQL Server, arquivos CSV/Excel).

**Casos de uso reais:**
- Sincronização Totalbus ↔ SAP (Grupo Comporte)
- Extração de dados de sistemas legados para BI (Targit / Tableau)
- Carga incremental com controle de duplicatas

---

## 🔍 log-analyzer

Parser de logs para investigação de causa raiz (RCA) de incidentes em ambientes de telecomunicações. Desenvolvido para análise de fluxos do Orchestrator Ascendon.

**Funcionalidades:**
- Parsing de logs em múltiplos formatos (JSON, texto estruturado, syslog)
- Correlação de eventos por `transaction_id` entre sistemas
- Timeline visual do fluxo do incidente
- Exportação de relatório de RCA em Markdown/HTML

```bash
python log_analyzer.py --input ./logs/ --trace-id "TXN-20260501-001" --output rca_report.html
```

---

## 🚀 Como usar

```bash
# Clone o repositório
git clone https://github.com/SEU_USUARIO/automacoes-python.git
cd automacoes-python

# Ambiente virtual
python -m venv venv
source venv/bin/activate

# Instale as dependências do módulo desejado
cd oauth-token-manager
pip install -r requirements.txt

# Execute os testes
pytest tests/ -v
```

---

## 📋 Pré-requisitos

- Python 3.10+
- Acesso às APIs/sistemas que serão integrados
- Variáveis de ambiente configuradas (ver `.env.example` em cada módulo)

---

## 🤝 Contexto profissional

Estas automações foram desenvolvidas durante atuação em:

- **Hitss Brasil / MVNO Nubank Claro** (2024–presente) — automações operacionais em Python
- **Grupo Comporte** (2020–2024) — ETL, integração SAP, automação UiPath
- **Linx S.A.** (2016–2019) — scripts de suporte à implantação de ERP

---

## 👤 Autor

**Gustavo Miranda**  
Desenvolvedor de Automação | Inteligência Operacional | Full Stack  
📍 São Bernardo do Campo, SP — Remoto  
🔗 [LinkedIn](https://www.linkedin.com/in/gustavo-miranda-84178bb5/)
