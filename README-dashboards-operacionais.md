# 📊 Dashboards Operacionais — Ferramentas Web Internas

> Templates e ferramentas de interface web desenvolvidas para equipes de operação — sem frameworks complexos, focadas em clareza, velocidade e uso imediato.

---

## 💡 Filosofia

Ferramentas operacionais precisam ser:
- **Rápidas de usar** — 1 campo, 1 clique, resultado na tela
- **Claras** — status visual imediato, sem ambiguidade
- **Leves** — HTML + CSS + JS vanilla, sem build step, sem dependências
- **Fáceis de manter** — qualquer dev consegue entender e modificar

Nada de frameworks pesados para uma tela interna. Menos é mais.

---

## 📂 Estrutura

```
dashboards-operacionais/
├── 📁 mesa-consulta/           # Interface de consulta unificada (base da Mesa MVNO)
├── 📁 monitor-apis/            # Dashboard de saúde de APIs em tempo real
├── 📁 status-board/            # Board de status operacional por sistema
├── 📁 rca-template/            # Template HTML para relatórios de RCA
├── 📁 sla-tracker/             # Tracker de SLA com alertas visuais
└── 📁 components/              # Componentes reutilizáveis (tabelas, badges, cards)
```

---

## 🖥️ mesa-consulta

Interface de consulta unificada — o padrão de UI usado na **Mesa de Operação MVNO**.

**Características:**
- Campo de busca único com validação em tempo real
- Consulta paralela a múltiplos backends
- Status visual por sistema (✅ OK · ⚠️ Lento · ❌ Erro)
- Resultado expandível por seção
- Zero dependências externas

```
┌─────────────────────────────────────────────┐
│  🔍  Digite o MSISDN ou ID                  │
│      [___________________________] [Buscar]  │
└─────────────────────────────────────────────┘

Resultados:
┌──────────────┬────────────┬──────────────────┐
│ Sistema      │ Status     │ Dados            │
├──────────────┼────────────┼──────────────────┤
│ Ascendon     │ ✅ 342ms   │ ACTIVE · Cycle 7 │
│ ECMS         │ ✅ 178ms   │ Plano: Nubank 40 │
│ PCF          │ ✅ 201ms   │ Perfil: PREPAGO  │
│ OCS          │ ✅ 156ms   │ Saldo: R$ 12,50  │
│ SPSWeb       │ ✅ 1.8s    │ Status: REGULAR  │
└──────────────┴────────────┴──────────────────┘
```

---

## 📡 monitor-apis

Dashboard em tempo real para monitoramento de APIs — atualização automática a cada N segundos.

```html
<!-- Uso básico: só aponte para seu backend -->
<script>
  const APIS = [
    { name: 'Ascendon',  url: '/api/health/ascendon' },
    { name: 'ECMS',      url: '/api/health/ecms'     },
    { name: 'PCF',       url: '/api/health/pcf'      },
  ];
  const INTERVAL_MS = 30000; // atualiza a cada 30s
</script>
```

**Métricas exibidas por API:**
- Status atual (UP / DEGRADED / DOWN)
- Tempo médio de resposta (últimas 10 chamadas)
- Uptime das últimas 24h
- Último incidente registrado

---

## 📋 rca-template

Template HTML para geração de relatórios de RCA (Root Cause Analysis) — usado para documentar incidentes em ambiente MVNO.

**Seções do template:**
1. Resumo executivo (impacto, duração, sistemas afetados)
2. Timeline do incidente
3. Análise de causa raiz
4. Sistemas e logs analisados
5. Ações corretivas tomadas
6. Ações preventivas recomendadas

```bash
# Gera relatório preenchido a partir de dados JSON
python rca-template/generate.py --data incident_data.json --output rca_2026_05_01.html
```

---

## ⏱️ sla-tracker

Tracker visual de SLA com alertas de proximidade ao limite:

```
Chamado #2026-0501   [████████░░░░░░░░░░░░] 40% do SLA  ✅ 3h restantes
Chamado #2026-0498   [████████████████░░░░] 80% do SLA  ⚠️ 1h restante
Chamado #2026-0491   [████████████████████] SLA VENCIDO  ❌
```

---

## 🧩 Componentes reutilizáveis

### Badge de status
```html
<span class="badge badge--ok">ATIVO</span>
<span class="badge badge--warning">DEGRADADO</span>
<span class="badge badge--error">INATIVO</span>
```

### Card de métrica
```html
<div class="metric-card">
  <span class="metric-value">342ms</span>
  <span class="metric-label">Tempo médio</span>
</div>
```

### Tabela com sorting
```html
<table class="ops-table" data-sortable>
  <thead>...</thead>
  <tbody>...</tbody>
</table>
<script src="components/sortable-table.js"></script>
```

---

## 🚀 Como usar

Todas as ferramentas são **arquivos estáticos** — sem build, sem servidor de desenvolvimento:

```bash
git clone https://github.com/SEU_USUARIO/dashboards-operacionais.git
cd dashboards-operacionais

# Abre direto no navegador (para interfaces sem backend)
open mesa-consulta/index.html

# Ou sobe um servidor local simples
python -m http.server 8080
# Acesse http://localhost:8080/mesa-consulta/
```

Para as ferramentas que precisam de backend (monitor-apis, sla-tracker):
```bash
cd monitor-apis
pip install -r requirements.txt
python server.py
```

---

## 🎨 Design system interno

Cores e variáveis CSS usadas em todos os componentes:

```css
:root {
  --ok:       #3be08b;   /* verde — sistema operacional */
  --warning:  #f5a623;   /* âmbar — degradado / lento */
  --error:    #ff4d4d;   /* vermelho — indisponível */
  --info:     #5ac8fa;   /* azul — informativo */
  --bg:       #0e1318;   /* fundo escuro */
  --surface:  #161d25;   /* superfície de cards */
  --text:     #e8f0f8;   /* texto principal */
  --muted:    #7e9ab5;   /* texto secundário */
}
```

---

## 👤 Autor

**Gustavo Miranda**  
Desenvolvedor de Automação | Inteligência Operacional | Full Stack  
📍 São Bernardo do Campo, SP — Remoto  
🔗 [LinkedIn](https://www.linkedin.com/in/gustavo-miranda-84178bb5/)
