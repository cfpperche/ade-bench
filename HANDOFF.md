# Handoff — ADE Bench

Atualizado em 2026-09-22, na migração `tachyon-ade-bench` → `ade-bench`
(produto de referência: Tachyon → PiCode).

## Estado atual

- Repositório renomeado para `ade-bench` (local e remoto); Pages em
  `https://cfpperche.github.io/ade-bench/`.
- Produto de referência do bench: **PiCode** (`~/picode`, read-only).
- `competitors/tachyon.json` foi removido; o perfil derivado agora é
  `competitors/picode.json`, alimentado por `docs/product/capabilities.json`
  via `scripts/product/sync-picode-profile.py`.
- Artefatos do período Tachyon ficam em `reports/archive/` e em `runs/`
  (gitignored), como registro histórico — não são reescritos.

## Evidência de validação

- `python3 harness/bench.py check`
- `python3 scripts/product/check-capabilities.py`
- `python3 scripts/intelligence/check-intelligence.py`
- `python3 scripts/marketing/check-marketing.py`
- `bash scripts/check-suite.sh`
- `python3 harness/test_inspect.py`
- `npm run dashboard:check` + `npm run dashboard:build`

## Comandos de retomada

```sh
cd /home/goat/ade-bench
git status --short
python3 harness/bench.py check
python3 harness/bench.py list-products | grep picode
```

## Limites

- `/home/goat/picode` e `/home/goat/tachyon` são somente leitura.
- Não transformar claims de marketing em evidência de benchmark.
- `runs/` é gitignored; manter evidência local salvo pedido explícito.
- Fazer commit/push somente quando o usuário autorizar.
