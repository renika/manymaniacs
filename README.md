# 🧠 ManyOne + Trafega

### Infraestrutura de Presença, Comunicação Contextual e Continuidade Digital

> Este projeto segue os princípios fundadores descritos no [MANIFESTO.md](./MANIFESTO.md)  
> e é guiado pelos compromissos estabelecidos em [ETHICS.md](./ETHICS.md).

---

## 🚀 Visão Geral

**ManyOne + Trafega** é um ecossistema modular para criar redes resilientes e sistemas que continuam funcionando mesmo sem internet, com foco em:

- 🧭 Comunicação Omnichannel inteligente
- 🧠 IA embarcada com cache seletivo
- 🔐 Segurança Zero Trust
- 📦 Ciclo de dados com staging e arquivamento
- 🌐 Operação local + sincronização inteligente
- 💬 Chat interno auditável e descentralizado
- 🌱 Presença Digital mesmo em ambientes offline

---

## 🔄 Ciclo de Vida do Dado

| Etapa         | Descrição                                                                 |
|---------------|---------------------------------------------------------------------------|
| **Ativo**     | Dado recente e usado frequentemente → mora no banco (PostgreSQL)          |
| **Staging**   | Dados menos usados → carregados sob demanda (RAM/disk)                    |
| **Arquivado** | Dados antigos → compactados e criptografados (JSONL, ZST, Parquet, etc.)  |
| **Nível Master** | Dado com +365 dias → acesso só com requisição formal e registro auditável |

---

## 🛠 Tecnologias Envolvidas

| Camada             | Uso Principal                                      |
|--------------------|----------------------------------------------------|
| `Phoenix`          | API, comunicação interna, websocket seguro         |
| `PostgreSQL`       | Dados ativos                                        |
| `DuckDB/SQLite`    | Consulta de arquivos arquivados                     |
| `Zstandard (ZST)`  | Compressão rápida e leve para dados frios          |
| `Task.Supervisor`  | TTL, expiração e limpeza de staging automatizado   |

---

## 🔐 Segurança e Ética

- JWT com autenticação forte e controle por dispositivo
- Central de Segurança para gestão de sessões e dispositivos conectados
- Permissões por função e tenant com controle por escopo
- Auditado e reversível: nenhum dado é excluído sem rastreio
- Cache local com base em contexto e presença

Leia mais em [ETHICS.md](./ETHICS.md)

---

## 💡 IA Embarcada com Cache Seletivo

A IA embarcada localmente:

- Acessa apenas dados relevantes via `staging`
- Trabalha offline com inferência baseada em contexto
- É limitada por lógica ternária: `1 = permitido`, `0 = requer interação`, `-1 = vetado`
- Não acessa dados master ou confidenciais sem autorização
- Não decide sozinha — apenas sugere e apoia

---

## 📦 Componentes do Sistema

| Componente         | Função Principal                                          |
|--------------------|-----------------------------------------------------------|
| `Omni Channel`     | Comunicação 1:1 com controle de chatbot e canais ativos   |
| `Storage Seguro`   | Upload seguro com antivírus, sandbox e antifraude         |
| `Chat Interno`     | Canal interno com criptografia e rastreio                 |
| `Assistente IA`    | Suporte contextual, offline-first                         |
| `Automação`        | Eventos e workflows acionados por contexto e presença     |

---

## 🧪 Exemplos de Comando (Pseudocódigo Elixir)

```elixir
Staging.load(:file_id)
Staging.drop(:file_id)

Archive.mark_candidate(:event_id)
Archive.finalize(:file_id)

Audit.log_access(:user, :file_id)
