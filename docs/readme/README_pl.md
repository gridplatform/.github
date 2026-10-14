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

Grid pomaga **samodzielnie prosić o, przeglądać i uruchamiać infrastrukturę chmurową** — bez zamykania setupu w cudzym produkcie. Opisujesz, czego chcesz, zatwierdzasz zmiany z jasną historią i trzymasz dostęp oraz zapisy na maszynach i w magazynie pod **Twoją** kontrolą.

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

Grid to miejsce, gdzie zespół **prosi o zasoby chmurowe** i **widzi, co naprawdę się zmieniło**.

Zapisujesz, czego chcesz — sieć, serwer, bazę — w plikach konfiguracji w repozytorium GitHub, które **należy do Ciebie**. Grid czyta ten opis, pokazuje plan zmian i po Twojej zgodzie tworzy lub usuwa te zasoby w Twojej chmurze. Każda zmiana trafia do release’u z logami na żywo, żeby inni mogli śledzić i zajrzeć później.

Uruchamiasz Grid na sprzęcie pod **Twoją** kontrolą. Dostęp do chmury zostaje przy tożsamości tej maszyny — w konfiguracjach nie potrzeba haseł ani kluczy. Jeśli maszynę później wymienisz, zapis tego, czym Grid zarządza, zostaje w zdalnym magazynie ustawionym raz.

Krótko: powiedz, czego chcesz, przejrzyj plan, zastosuj ze śladem, któremu ufasz.

## Twój desired state

**[grid-config](https://github.com/gridplatform/grid-config) to tylko przykład.** Użyj go, by zobaczyć, jak wyglądają konfiguracje. **Nie** forkuј do prawdziwego środowiska.

Dla własnego setupu:

1. Utwórz **nowe** repozytorium GitHub w swojej org lub koncie.
2. Umieść własne pliki konfiguracji (czego chcesz w każdym środowisku).
3. Wskaż Grid na **to** repository — nie na `grid-config`.

Bierz pomysły z przykładu; własność repository i ustawień zostaw sobie.

## Repozytoria

| Repozytorium | Do czego to służy |
|------------|---------------|
| [grid-core](https://github.com/gridplatform/grid-core) | Uruchamia Grid na Twojej maszynie — silnik w tle i sposób instalacji |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Strona, której używasz w przeglądarce |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Ta sama praca z terminala, bez otwierania strony |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Gotowe elementy typowych zasobów chmurowych (sieci, serwery i inne) |
| [grid-config](https://github.com/gridplatform/grid-config) | Przykładowe konfiguracje do nauki — **nie** Twój prawdziwy setup (załóż własne repozytorium) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Przewodniki prostym językiem |

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

Zforkuj repository **produktowe** (core, ui, cli, terraform, docs) → gałąź → PR do `main`.  
Nie traktuj `grid-config` jako prywatnego domu desired-state.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## Licencja

MIT — see each repository’s `LICENSE`.
