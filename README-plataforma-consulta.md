# 🖥️ Plataforma Unificada de Consulta

> Interface unificada para consultas e validações em uma **operação de alta complexidade** — desenvolvida para transformar um processo de 20 minutos em menos de 2.

---

## 📊 Impacto

| Métrica | Resultado |
|---|---|
| ⏱️ Tempo por consulta | De 15–20 min → **menos de 2 min** |
| 💰 Horas economizadas | **~200h/mês** para a equipe |
| 🔗 Sistemas integrados | **6 sistemas** simultâneos |
| 👥 Adoção | Qualquer pessoa da equipe consegue operar — sem conhecer as APIs |

---

## 🧩 O Problema

No dia a dia da operação, cada consulta de aprovisionamento exigia um processo totalmente manual:

- ❌ Gerar **3 tokens OAuth** manualmente (um por sistema)
- ❌ Coletar dados no **sistema de origem** um a um
- ❌ Chamar **5 APIs separadas** com dados copiados entre telas
- ❌ Comparar **parâmetros críticos entre sistemas** na mão, sujeito a erro humano
- ❌ Abrir e navegar em um **sistema complementar** manualmente
- ⏱️ **Total: 15 a 20 minutos por consulta**

Além do tempo perdido, o processo exigia que o operador conhecesse todas as APIs, fluxos e sistemas envolvidos — criando dependência de especialistas.

---

## ✅ A Solução

A **Plataforma Unificada de Consulta** é uma plataforma web interna que centraliza tudo em **1 campo + 1 clique**:

- ✅ Token OAuth gerado automaticamente (sem intervenção manual)
- ✅ 6 sistemas consultados em paralelo e simultaneamente
- ✅ Parâmetros críticos validados e cruzados automaticamente entre sistemas
- ✅ Sistema complementar navegado via **Playwright** (automação de browser headless)
- ✅ Resultado completo apresentado com **status visual** por sistema
- ⚡ **Total: menos de 2 minutos**

---

## 🛠️ Stack

```
Backend      → Python · FastAPI
Automação    → Playwright (browser headless)
Auth         → OAuth 2.0 (geração automática de tokens)
Frontend     → HTML · CSS · JavaScript (vanilla)
Integração   → APIs REST e automação de sistema web complementar
```

---

## 🏗️ Arquitetura

```
┌─────────────────────────────────────────┐
│            Interface Web (HTML/JS)       │
│         1 campo de busca · 1 clique     │
└────────────────────┬────────────────────┘
                     │
              FastAPI Backend
                     │
        ┌────────────┼────────────┐
        │            │            │
   OAuth Manager  Playwright   API Router
   (auto-token)   (Web app)  (REST calls)
        │            │            │
   ┌────┴────┐   ┌───┴───┐   ┌───┴────────────┐
   │Sistema A│   │Web app│   │ Sistemas B·C·D │
   └─────────┘   └───────┘   └────────────────┘
        │
   Critical Data Validator
   (cross-system comparison)
```

---

## 🚀 Como executar

```bash
# Clone o repositório
git clone https://github.com/SEU_USUARIO/plataforma-consulta.git
cd plataforma-consulta

# Crie o ambiente virtual
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Instale as dependências
pip install -r requirements.txt

# Instale o browser para o Playwright
playwright install chromium

# Configure as variáveis de ambiente
cp .env.example .env
# Edite o .env com suas credenciais

# Rode o servidor
uvicorn main:app --reload
```

Acesse `http://localhost:8000` no navegador.

---

## ⚙️ Variáveis de ambiente

```env
# Credenciais de autenticação
CLIENT_ID=seu_client_id
CLIENT_SECRET=seu_client_secret

# URLs dos sistemas (configuráveis por ambiente)
SOURCE_SYSTEM_URL=https://...
ECMS_URL=https://...
PCF_URL=https://...
OCS_URL=https://...
WEB_APP_URL=https://...

# Configurações gerais
TOKEN_REFRESH_INTERVAL=3600
LOG_LEVEL=INFO
```

---

## 📁 Estrutura do projeto

```
plataforma-consulta/
├── main.py                  # Entry point FastAPI
├── requirements.txt
├── .env.example
├── app/
│   ├── auth/
│   │   └── oauth.py         # Geração automática de tokens
│   ├── integrations/
│   │   ├── source_system.py # Consultas ao sistema de origem
│   │   ├── system_b.py
│   │   ├── system_c.py
│   │   ├── system_d.py
│   │   └── web_app.py       # Automação Playwright
│   ├── validators/
│   │   └── critical_data.py # Validação cruzada de dados críticos
│   └── routers/
│       └── consulta.py      # Endpoints da API
├── frontend/
│   ├── index.html
│   ├── style.css
│   └── app.js
└── docs/
    └── architecture.md
```

---

## 📈 Resultados em produção

Este projeto está em produção desde **maio de 2026**, com adoção total da equipe e os seguintes resultados mensurados:

- Redução de **90%** no tempo médio por consulta
- Eliminação de erros por copy-paste manual entre sistemas
- Democratização do processo — qualquer operador executa sem treinamento técnico avançado
- Liberação de ~**200 horas mensais** da equipe para atividades de maior valor

---

## 👤 Autor

**Gustavo Miranda**  
Especialista em Automação e IA Aplicada | Integração de Sistemas<br>
📍 São Bernardo do Campo, SP — Remoto  
🔗 [LinkedIn](https://www.linkedin.com/in/gustavo-miranda-84178bb5/)
