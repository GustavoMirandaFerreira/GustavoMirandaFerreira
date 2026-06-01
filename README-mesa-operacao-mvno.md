# 🖥️ Mesa de Operação MVNO

> Interface de consulta unificada para aprovisionamento da operação **MVNO Nubank Claro** — desenvolvida para transformar um processo de 20 minutos em menos de 2.

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

No dia a dia da operação MVNO, cada consulta de aprovisionamento exigia um processo totalmente manual:

- ❌ Gerar **3 tokens OAuth** manualmente (um por sistema)
- ❌ Coletar dados no **Ascendon** um a um
- ❌ Chamar **5 APIs separadas** com dados copiados entre telas
- ❌ Comparar **CycleDays entre sistemas** na mão, sujeito a erro humano
- ❌ Abrir e navegar no **SPSWeb** manualmente
- ⏱️ **Total: 15 a 20 minutos por consulta**

Além do tempo perdido, o processo exigia que o operador conhecesse todas as APIs, fluxos e sistemas envolvidos — criando dependência de especialistas.

---

## ✅ A Solução

A **Mesa de Operação MVNO** é uma plataforma web interna que centraliza tudo em **1 campo + 1 clique**:

- ✅ Token OAuth gerado automaticamente (sem intervenção manual)
- ✅ 6 sistemas consultados em paralelo e simultaneamente
- ✅ CycleDays validados e cruzados automaticamente entre sistemas
- ✅ SPSWeb navegado via **Playwright** (automação de browser headless)
- ✅ Resultado completo apresentado com **status visual** por sistema
- ⚡ **Total: menos de 2 minutos**

---

## 🛠️ Stack

```
Backend      → Python · FastAPI
Automação    → Playwright (browser headless)
Auth         → OAuth 2.0 (geração automática de tokens)
Frontend     → HTML · CSS · JavaScript (vanilla)
Integração   → APIs REST (Ascendon · ECMS · PCF · OCS · SPSWeb)
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
   (auto-token)   (SPSWeb)   (REST calls)
        │            │            │
   ┌────┴────┐   ┌───┴───┐   ┌───┴────────────┐
   │ Ascendon│   │SPSWeb │   │ ECMS·PCF·OCS   │
   └─────────┘   └───────┘   └────────────────┘
        │
   CycleDays Validator
   (cross-system comparison)
```

---

## 🚀 Como executar

```bash
# Clone o repositório
git clone https://github.com/SEU_USUARIO/mesa-operacao-mvno.git
cd mesa-operacao-mvno

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
ASCENDON_URL=https://...
ECMS_URL=https://...
PCF_URL=https://...
OCS_URL=https://...
SPSWEB_URL=https://...

# Configurações gerais
TOKEN_REFRESH_INTERVAL=3600
LOG_LEVEL=INFO
```

---

## 📁 Estrutura do projeto

```
mesa-operacao-mvno/
├── main.py                  # Entry point FastAPI
├── requirements.txt
├── .env.example
├── app/
│   ├── auth/
│   │   └── oauth.py         # Geração automática de tokens
│   ├── integrations/
│   │   ├── ascendon.py      # Consultas Ascendon
│   │   ├── ecms.py
│   │   ├── pcf.py
│   │   ├── ocs.py
│   │   └── spsweb.py        # Automação Playwright
│   ├── validators/
│   │   └── cycledays.py     # Validação cruzada CycleDays
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

Este projeto está em uso na operação MVNO Nubank Claro desde **maio de 2026**, com adoção total da equipe e os seguintes resultados mensurados:

- Redução de **90%** no tempo médio por consulta
- Eliminação de erros por copy-paste manual entre sistemas
- Democratização do processo — qualquer operador executa sem treinamento técnico avançado
- Liberação de ~**200 horas mensais** da equipe para atividades de maior valor

---

## 👤 Autor

**Gustavo Miranda**  
Desenvolvedor de Automação | Inteligência Operacional | Full Stack  
📍 São Bernardo do Campo, SP — Remoto  
🔗 [LinkedIn](https://www.linkedin.com/in/gustavo-miranda-84178bb5/)
