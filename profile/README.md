# 배리어프리 웹툰 뷰어 (boin-bf-webtoon-viewer)

국립장애인도서관 배리어프리 웹툰 **열람·패키징·배포**를 위한 코드 조직입니다.

## 한눈에 보기

원본 웹툰을 **포렌식 워터마크(0/1) → 스크램블 아틀라스 → 마스터 정답지**로 패키징하고,  
뷰어는 EPUB에서 암호 정답지만 백엔드로 보내 **개인화 정답지**를 받아 화면에 조립합니다.  
CEK·라이선스·대여 entitlement는 서버 측에서 다루며, 클라이언트에는 마스터 정답지 평문을 두지 않는 흐름을 목표로 합니다.

```text
제작(패키징)  →  저장/카탈로그  →  포털 로그인  →  뷰어 열람
                    ↑                ↑              ↑
              AMPAS / 메타      auth 포털      FE + BE resolve
```

## 저장소 안내

| 저장소 | 역할 |
|--------|------|
| [bf_webtoon_frontend](https://github.com/boin-bf-webtoon-viewer/bf_webtoon_frontend) | 웹툰 **뷰어 SPA** (캔버스 조립·재생·admission) |
| [bf_webtoon_backend](https://github.com/boin-bf-webtoon-viewer/bf_webtoon_backend) | 뷰어 **API** (EPUB 제공, 정답지 resolve, LCP/CEK) |
| [bf_webtoon_authTest](https://github.com/boin-bf-webtoon-viewer/bf_webtoon_authTest) | **포털·로그인·handoff** 시연용 auth (데모 entitlement) |
| [bf_webtoon_ampas](https://github.com/boin-bf-webtoon-viewer/bf_webtoon_ampas) | 콘텐츠·패키지 **저장소(AMPAS) 연동** 자리 |
| [bf_webtoon_webtoontoEncEpu](https://github.com/boin-bf-webtoon-viewer/bf_webtoon_webtoontoEncEpu) | **WM·아틀라스·정답지** 패키징 파이프라인 |
| [LCP_TEST](https://github.com/boin-bf-webtoon-viewer/LCP_TEST) | EPUB **LCP 암호화** · 메타데이터 카탈로그 |
| [bf-contentsToEPUB](https://github.com/boin-bf-webtoon-viewer/bf-contentsToEPUB) | CMS export → **평문 EPUB** 변환 |

## 권장 읽기 순서

1. **제작:** `bf-contentsToEPUB` → `bf_webtoon_webtoontoEncEpu` → (`LCP_TEST`)  
2. **열람:** `bf_webtoon_authTest` → `bf_webtoon_frontend` + `bf_webtoon_backend`  
3. **납품/저장:** `bf_webtoon_ampas`

## 참고

- 대부분 Private 저장소입니다. 권한은 조직 People/Teams에서 관리합니다.  
- 로컬·배포 상세는 각 저장소 README와 모노레포 `doc/` 문서를 따릅니다.  
- 이 페이지는 조직 Overview 표지용입니다 (`.github` / `profile/README.md`).
