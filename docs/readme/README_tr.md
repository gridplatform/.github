<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · **Türkçe** · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### Kendi barındırdığınız altyapı orkestrasyonu — desired-state JSON, Terraform modülleri, denetlenebilir release’ler.

**Kontrol düzleminiz. Kimlik bilgileriniz. State’iniz.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[Hızlı başlangıç](#hızlı-başlangıç) · [Nasıl çalışır](#nasıl-çalışır) · [Desired state’iniz](#desired-state’iniz) · [Depolar](#depolar) · [Dokümantasyon](#dokümantasyon)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid, yol biçimli altyapı JSON’unu genel bir modül bankası üzerinden Terraform’a dönüştürür, **plan / apply / destroy** işlemlerini denetlenebilir **release** olarak çalıştırır ve GitOps tarzı bir konsol sunar. VM veya Docker Compose ile self-host — satıcı kilidi yok, düz Terraform çıkışı.

> **Demo videosu** — yakında.

## Hızlı başlangıç

1. **[Uzak Terraform state](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** oluşturun (S3 / GCS / Azure).
2. Grid’i bir VM’e kurun (varsayılan Compose).

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

`http://<host>/` adresini açın. Uzun ömürlü bulut anahtarları yerine VM’de **instance role / service account** tercih edin.

Tam yol: **[VM’e kurulum](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**.

## Nasıl çalışır

| Parça | Rol |
|-------|------|
| **Sizin** desired-state deponuz | **Sizin** oluşturduğunuz GitHub deposu — ne deploy edeceğinizin JSON’u |
| Modül bankası | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | API, GitOps senkronu, release + canlı loglar |
| grid-ui | Konsol |

Bulut izinleri **host kimliğinden** gelir (AWS instance role / GCP ADC). Desired-state dosyaları kimlik bilgisi taşımaz. Üretim uzak state kullanır; VM değişince Terraform haritası kaybolmaz.

## Desired state’iniz

**[grid-config](https://github.com/gridplatform/grid-config) yalnızca örnektir.** JSON şeklini öğrenmek için okuyun. Üretim için **fork etmeyin**.

Gerçek bir deploy için:

1. Org veya hesabınızda **yeni** bir GitHub deposu oluşturun.
2. Kendi yol biçimli JSON’unuzu ekleyin (provider / env / kaynak birimleri).
3. Grid’i o depoya yönlendirin (`GRID_GITOPS_REPO_URL`) — `grid-config`’e değil.

Örnekten kalıpları kopyalayın; depo ve ayarlar size aittir.

## Depolar

| Repo | Rol |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Konsol |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate → plan → apply → destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| [grid-config](https://github.com/gridplatform/grid-config) | **Örnek** desired-state (üretim fork’unuz değil) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Dokümantasyon |

Bitti / devam ediyor / planlandı: **[STATUS.md](../../STATUS.md)**.

## Dokümantasyon

| Rehber | Bağlantı |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## Katkıda bulunma

Bir **ürün** deposunu fork edin (core, ui, cli, terraform, docs) → dal → `main`’e PR.  
`grid-config`’i özel desired-state eviniz gibi kullanmayın.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## Lisans

MIT — see each repository’s `LICENSE`.
