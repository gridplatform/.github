<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · **한국어** · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### 셀프호스팅 인프라 오케스트레이션 — desired-state JSON, Terraform 모듈, 감사 가능한 릴리스.

**당신의 컨트롤 플레인. 당신의 자격 증명. 당신의 상태.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[빠른 시작](#빠른-시작) · [동작 방식](#동작-방식) · [당신의 desired state](#당신의-desired-state) · [저장소](#저장소) · [문서](#문서)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid는 **클라우드 인프라를 직접 요청·검토·실행**하도록 돕습니다. 설정을 다른 제품에 가두지 않습니다. 원하는 것을 적고, 이력이 남는 변경을 승인하며, 접근과 기록은 **당신**이 통제하는 장비와 저장소에 둡니다.

> **데모 영상** — 곧 공개.

## 빠른 시작

1. **[원격 Terraform 상태](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** 생성 (S3 / GCS / Azure).
2. VM에 Grid 설치 (기본 Compose).

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

`http://<host>/` 열기. 장기 클라우드 키보다 VM의 **인스턴스 역할 / 서비스 계정**을 권장.

전체 경로: **[VM에 설치](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**.

## 동작 방식

Grid는 팀이 **클라우드 자원을 요청**하고 **실제로 무엇이 바뀌었는지 보는** 곳입니다.

네트워크, 서버, 데이터베이스 등 원하는 것을 **당신 소유의** GitHub 저장소 설정 파일에 적습니다. Grid가 그 설명을 읽고 무엇이 바뀔지 계획을 보여 주며, 승인하면 당신 클라우드에서 만들거나 지웁니다. 모든 변경은 실시간 로그가 있는 릴리스로 남아, 따라보거나 나중에 다시 볼 수 있습니다.

Grid는 **당신이** 통제하는 장비에서 돌아갑니다. 클라우드 접근은 그 장비의 신원에 머물며 — 설정 파일에 비밀번호나 키를 넣을 필요가 없습니다. 나중에 장비를 바꿔도, Grid가 관리하는 것의 기록은 처음에 마련한 원격 저장소에 남습니다.

한 줄로: 원하는 것을 말하고, 계획을 검토하고, 믿을 수 있는 이력과 함께 적용하세요.

## 당신의 desired state

**[grid-config](https://github.com/gridplatform/grid-config)는 예시일 뿐입니다.** 설정이 어떻게 생겼는지 보는 용도입니다. 실제 환경용으로 **fork 하지 마세요**.

당신 환경에서는:

1. 조직/계정에 **새** GitHub 저장소를 만듭니다.
2. 자신의 설정 파일을 넣습니다 (환경마다 원하는 것).
3. Grid를 **그** 저장소로 가리킵니다 — `grid-config`가 아닙니다.

예시에서 아이디어를 빌리고, 저장소와 설정은 직접 소유하세요.

## 저장소

| 저장소 | 무엇을 위한 것인가 |
|------------|---------------|
| [grid-core](https://github.com/gridplatform/grid-core) | 당신 장비에서 Grid를 돌리는 엔진 — 그리고 설치 방법 |
| [grid-ui](https://github.com/gridplatform/grid-ui) | 브라우저에서 쓰는 웹사이트 |
| [grid-cli](https://github.com/gridplatform/grid-cli) | 웹사이트 없이 터미널에서 같은 일을 하는 도구 |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | 흔한 클라우드 자원을 위한 준비된 조각 (네트워크, 서버 등) |
| [grid-config](https://github.com/gridplatform/grid-config) | 배우기용 샘플 설정 — 실제 환경이 **아님** (직접 저장소를 만드세요) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | 쉬운 말로 쓴 가이드 |

완료 / 진행 중 / 계획: **[STATUS.md](../../STATUS.md)**.

## 문서

| 가이드 | 링크 |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## 기여

**제품** 저장소(core, ui, cli, terraform, docs)를 fork → 브랜치 → `main`에 PR.  
`grid-config`를 개인 desired-state 저장소로 쓰지 마세요.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

이슈: [grid-core](https://github.com/gridplatform/grid-core/issues).

## 라이선스

MIT — see each repository’s `LICENSE`.
