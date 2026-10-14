<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · **Türkçe** · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### Self-hosted altyapı orkestrasyon platformu.

**Kurumların altyapıyı dağıtıp yönetmesi için — kontrol sizde kalsın diye.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[Hızlı başlangıç](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md) · [Nasıl çalışır](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) · [Desired state’iniz](https://github.com/gridplatform/grid-config#readme) · [Depolar](https://github.com/orgs/gridplatform/repositories) · [Dokümantasyon](https://github.com/gridplatform/grid-docs)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid, bulut altyapısını dağıtmak ve işletmek için **self-hosted** bir platformdur. Kurumlar nasıl yayınlandığını, kimin değiştirebileceğini ve erişimin nerede durduğunu kendilerinde tutar — bu kontrolü başka bir sağlayıcının konsoluna vermeden.

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

Grid, ekibinizin **bulut kaynakları istemek** ve **gerçekte neyin değiştiğini görmek** için gittiği yerdir.

İstediğinizi — ağ, sunucu, veritabanı — **size ait** bir GitHub deposundaki yapılandırma dosyalarına yazarsınız. Grid bu açıklamayı okur, neyin değişeceğinin planını gösterir; onayladığınızda bunları bulutunuzda oluşturur veya kaldırır. Her değişiklik canlı log’lu bir release olarak kaydedilir; başkaları takip edebilir, sonra geri bakabilir.

Grid’i **sizin** kontrolünüzdeki donanımda çalıştırırsınız. Bulut erişimi o makinenin kimliğinde kalır — yapılandırma dosyalarının içinde parola veya anahtar olması gerekmez. Makine sonra değiştirilirse, Grid’in yönettiği şeylerin kaydı bir kez kurduğunuz uzak depolamada kalır.

Kısaca: ne istediğinizi söyleyin, planı gözden geçirin, güvenebileceğiniz bir izle uygulayın.

## Desired state’iniz

**[grid-config](https://github.com/gridplatform/grid-config) yalnızca örnektir.** Yapılandırmaların nasıl göründüğünü görmek için kullanın. Gerçek ortamınız için **fork etmeyin**.

Kendi kurulumunuz için:

1. Org veya hesabınızda **yeni** bir GitHub deposu oluşturun.
2. Kendi yapılandırma dosyalarınızı koyun (her ortamda ne istediğiniz).
3. Grid’i **o** depoya yönlendirin — `grid-config`’e değil.

Örnekten fikir alın; deponun ve ayarların sahibi siz olun.

## Depolar

| Depo | Ne işe yarar |
|------------|---------------|
| [grid-core](https://github.com/gridplatform/grid-core) | Grid’i makinenizde çalıştırır — arkadaki motor ve kurulum |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Tarayıcıda kullandığınız web sitesi |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Aynı işi web sitesi açmadan terminalden yapan araç |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Sık kullanılan bulut kaynakları için hazır parçalar (ağlar, sunucular ve daha fazlası) |
| [grid-config](https://github.com/gridplatform/grid-config) | Öğrenmek için örnek ayarlar — gerçek kurulumunuz **değil** (kendi deponuzu oluşturun) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Sade dille yazılmış rehberler |

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
