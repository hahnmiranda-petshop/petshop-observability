# 📊 Petshop - Observability Stack

[![Docker](https://img.shields.io/badge/Docker-Compose-blue)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)]()

Stack de **observabilidade** para o projeto **Petshop**, utilizando **Prometheus**, **Grafana** e **Loki** para métricas e logs.  
O **Jaeger** poderá ser integrado futuramente para tracing distribuído.

---

## 📂 Estrutura do repositório
- `docker-compose.yml` → Serviços da stack de observabilidade
- `grafana/` → Dashboards e configurações provisionadas (datasources, pastas, etc.)
- `prometheus/` → Configurações de métricas
- `grafana/provisioning/datasources/` → Configuração automática dos datasources (**Prometheus** e **Loki**)

---

## 🚀 Como subir e parar a stack

```bash
# Subir
docker compose up -d

# Parar e remover containers
docker compose down
```

---

## 🩺 Testando os serviços

**Prometheus UI**  
[http://localhost:9090](http://localhost:9090)

**Grafana UI** (usuário/senha padrão: `admin` / `admin`)  
[http://localhost:3000](http://localhost:3000)

**Loki Health Check**
```bash
curl http://localhost:3100/ready
curl http://localhost:3100/loki/api/v1/status/buildinfo
```

> O Loki pode levar ~15 segundos para ficar pronto.  
> Enquanto isso, o endpoint `/ready` retornará `Ingester not ready`.

---

## 🔍 Datasources provisionados no Grafana

- **Prometheus** → Métricas (scrape a cada 15s)
- **Loki** → Logs (por padrão sem promtail; utilize queries no modo *Explore*)

> Para logs de teste, você pode descomentar o serviço `loki-canary` no `docker-compose.yml` e rodar a query:
```
{job="loki-canary"}
```

---

## 📌 Observações
- A stack atual **não** inclui o **Promtail** para ingestão de logs externos — será configurado quando os serviços do Petshop estiverem prontos para envio.
- O Jaeger e tracing distribuído serão adicionados em uma etapa futura.
- Datasources já vêm configurados automaticamente via `grafana/provisioning`.

---

## 🔗 Links úteis
- [Repositório principal (petshop)](https://github.com/hahnmiranda-petshop/petshop)
- [Kanban no GitHub Project](https://github.com/orgs/hahnmiranda-petshop/projects/1)

---

> 📜 Licença: [MIT](LICENSE)
