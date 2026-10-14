<div align="center">

[English](../../profile/README.md) · **हिन्दी** · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### स्वयं-होस्टेड इन्फ्रास्ट्रक्चर ऑर्केस्ट्रेशन प्लेटफ़ॉर्म।

**उद्यमों के लिए बनाया गया — इन्फ्रास्ट्रक्चर तैनात और संचालित करें, नियंत्रण अपने पास रखें।**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](../../LICENSE)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[त्वरित शुरुआत](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md) · [यह कैसे काम करता है](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) · [आपकी desired state](https://github.com/gridplatform/grid-config#readme) · [रिपॉज़िटरी](https://github.com/orgs/gridplatform/repositories) · [दस्तावेज़](https://github.com/gridplatform/grid-docs)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid एक **स्वयं-होस्टेड** प्लेटफ़ॉर्म है जिससे आप क्लाउड इन्फ्रास्ट्रक्चर तैनात और चला सकते हैं। उद्यम इसका उपयोग इसलिए करते हैं कि रोलआउट कैसे हो, कौन बदल सकता है, और पहुँच कहाँ रहे — यह नियंत्रण किसी और विक्रेता के कंसोल को सौंपे बिना अपने पास रहे।

> **डेमो वीडियो** — जल्द आ रहा है।

## त्वरित शुरुआत

1. **[रिमोट Terraform स्टेट](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** बनाएँ (S3 / GCS / Azure)।
2. VM पर Grid इंस्टॉल करें (डिफ़ॉल्ट Compose)।

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

`http://<host>/` खोलें। लंबे समय तक चलने वाली क्लाउड कुंजियों के बजाय VM पर **इंस्टेंस रोल / सर्विस अकाउंट** को प्राथमिकता दें।

पूरा मार्ग: **[VM पर इंस्टॉल](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**।

## यह कैसे काम करता है

Grid वह जगह है जहाँ आपकी टीम **क्लाउड संसाधन माँगती है** और **देखती है कि वास्तव में क्या बदला**।

आप जो चाहते हैं — नेटवर्क, सर्वर, डेटाबेस — उसे **अपनी** GitHub रिपॉज़िटरी की कॉन्फ़िग फ़ाइलों में लिखते हैं। Grid वह विवरण पढ़ता है, बदलाव की योजना दिखाता है, और जब आप स्वीकृत करते हैं तो आपके क्लाउड में बनाता या हटाता है। हर बदलाव लाइव लॉग वाले रिलीज़ के रूप में सहेजा जाता है, ताकि दूसरे साथ चल सकें और बाद में देख सकें।

आप Grid को **अपने** नियंत्रण वाले हार्डवेयर पर चलाते हैं। क्लाउड पहुँच उस मशीन की पहचान के साथ रहती है — कॉन्फ़िग में पासवर्ड या कुंजी रखने की ज़रूरत नहीं। बाद में मशीन बदल जाए तो Grid क्या प्रबंधित करता है, इसका रिकॉर्ड उस रिमोट स्टोरेज में रहता है जो आपने एक बार सेट किया।

संक्षेप में: बताएँ क्या चाहिए, योजना जाँचें, भरोसेमंद निशान के साथ लागू करें।

## आपकी desired state

**[grid-config](https://github.com/gridplatform/grid-config) केवल उदाहरण है।** कॉन्फ़िग कैसी दिखती है, यह देखने के लिए उपयोग करें। अपनी असली सेटअप के लिए इसे **fork न करें**।

अपनी सेटअप के लिए:

1. अपने org या खाते के तहत एक **नई** GitHub रिपॉज़िटरी बनाएँ।
2. अपनी कॉन्फ़िग फ़ाइलें वहाँ रखें (हर वातावरण में क्या चाहिए)।
3. Grid को **उस** रिपॉज़िटरी की ओर इंगित करें — `grid-config` की ओर नहीं।

उदाहरण से विचार लें; रिपॉज़िटरी और सेटिंग्स का स्वामित्व अपने पास रखें।

## रिपॉज़िटरी

| रिपॉज़िटरी | किस काम की है |
|------------|---------------|
| [grid-core](https://github.com/gridplatform/grid-core) | आपकी मशीन पर Grid चलाता है — पीछे का इंजन और इंस्टॉल का तरीका |
| [grid-ui](https://github.com/gridplatform/grid-ui) | ब्राउज़र में इस्तेमाल होने वाली वेबसाइट |
| [grid-cli](https://github.com/gridplatform/grid-cli) | वही काम टर्मिनल से, वेबसाइट खोले बिना |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | सामान्य क्लाउड संसाधनों के लिए तैयार टुकड़े (नेटवर्क, सर्वर आदि) |
| [grid-config](https://github.com/gridplatform/grid-config) | सीखने के लिए नमूना कॉन्फ़िग — **आपकी** असली सेटअप नहीं (अपनी रिपॉज़िटरी बनाएँ) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | सादी भाषा में गाइड |

पूर्ण / प्रगति पर / योजनाबद्ध: **[STATUS.md](../../STATUS.md)**।

## दस्तावेज़

| गाइड | लिंक |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## योगदान

किसी **उत्पाद** रिपॉज़िटरी (core, ui, cli, terraform, docs) को fork करें → शाखा → `main` पर PR।  
`grid-config` को अपनी निजी desired-state जगह न बनाएँ।

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## लाइसेंस

[MIT](../../LICENSE) © 2026 Grid Platform.

उत्पाद रिपॉज़िटरी (grid-core, grid-ui, grid-cli आदि) भी उन्हीं शर्तों वाली अपनी `LICENSE` रखती हैं।
