<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · **Polski** · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### Samodzielnie hostowana orkiestracja infrastruktury — JSON stanu pożądanego, moduły Terraform, audytowane release’y.

**Twoja control plane. Twoje poświadczenia. Twój stan.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[Szybki start](#szybki-start) · [Jak to działa](#jak-to-działa) · [Twój desired state](#twój-desired-state) · [Repozytoria](#repozytoria) · [Dokumentacja](#dokumentacja)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid zamienia path-shaped JSON infrastruktury w Terraform przez publiczny bank modułów, uruchamia **plan / apply / destroy** jako audytowane **release’y** i daje konsolę w stylu GitOps. Self-host na VM lub Docker Compose — bez vendor lock-in, wyjście czystym Terraformem.

> **Film demo** — wkrótce.

## Szybki start

1. Utwórz **[zdalny stan Terraform](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** (S3 / GCS / Azure).
2. Zainstaluj Grid na VM (domyślnie Compose).

```bash
export GRID_AUTH_ADMIN_PASSWORD='choose-a-strong-password'
# set GRID_TF_BACKEND / GRID_TF_STATE_BUCKET / … after remote state exists
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

```bash
git clone https://github.com/gridplatform/grid-core.git
cd grid-core
cp install/.env.example install/.env   # password + GRID_TF_*
docker compose -f install/docker-compose.yml --env-file install/.env up -d --build
```

Otwórz `http://<host>/`. Preferuj **rolę instancji / konto usługi** na VM zamiast długotrwałych kluczy chmurowych.

Pełna ścieżka: **[Instalacja na VM](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**.

## Jak to działa

| Element | Rola |
|-------|------|
| **Twoje** repo desired-state | Repozytorium GitHub, które **tworzysz** — JSON tego, co wdrażasz |
| Bank modułów | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | API, sync GitOps, release’y + logi na żywo |
| grid-ui | Konsola |

Uprawnienia chmurowe pochodzą z **tożsamości hosta** (rola instancji AWS / ADC GCP). Pliki desired-state nie niosą poświadczeń. Produkcja używa remote state, by wymiana VM nie gubiła mapy Terraform.

## Twój desired state

**[grid-config](https://github.com/gridplatform/grid-config) to tylko przykład.** Przeczytaj, by poznać kształt JSON. **Nie** forkuј do produkcji.

Dla prawdziwego wdrożenia:

1. Utwórz **nowe** repozytorium GitHub w swojej org lub koncie.
2. Dodaj własny path-shaped JSON (provider / env / jednostki zasobów).
3. Wskaż Grid na to repo (`GRID_GITOPS_REPO_URL`) — nie na `grid-config`.

Kopiuj wzorce z przykładu; repo i ustawienia należą do Ciebie.

## Repozytoria

| Repo | Rola |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Konsola |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate → plan → apply → destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| [grid-config](https://github.com/gridplatform/grid-config) | **Przykładowy** desired-state (nie Twój fork produkcyjny) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Dokumentacja |

Zrobione / w toku / planowane: **[STATUS.md](../../STATUS.md)**.

## Dokumentacja

| Przewodnik | Link |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## Współtworzenie

Zforkuj repo **produktowe** (core, ui, cli, terraform, docs) → gałąź → PR do `main`.  
Nie traktuj `grid-config` jako prywatnego domu desired-state.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## Licencja

MIT — see each repository’s `LICENSE`.
