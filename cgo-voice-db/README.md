# CGO Voice DB — 중앙 번역 허브

> CGO MESSAGE + CGO FULI 공용 번역 사전

## 📚 구조

```
cgo-voice-db/
├── dict/           번역 사전 (14 × 14 = 196 언어쌍)
│   ├── ko-KR_en-US.json
│   ├── ko-KR_ja-JP.json
│   └── ...
├── voice/          음성 파일 (기존)
│   └── ...
└── README.md
```

## 🌐 지원 언어 (14개국)

| 코드 | 언어 | 코드 | 언어 |
|------|------|------|------|
| ko-KR | 🇰🇷 한국어 | ru-RU | 🇷🇺 Русский |
| en-US | 🇺🇸 English | pt-BR | 🇧🇷 Português |
| ja-JP | 🇯🇵 日本語 | th-TH | 🇹🇭 ไทย |
| zh-CN | 🇨🇳 中文 | vi-VN | 🇻🇳 Tiếng Việt |
| es-ES | 🇪🇸 Español | ar-SA | 🇸🇦 العربية |
| fr-FR | 🇫🇷 Français | id-ID | 🇮🇩 Indonesia |
| de-DE | 🇩🇪 Deutsch |
| it-IT | 🇮🇹 Italiano |

## 🔗 사용 방법

### 앱에서 조회 (무서버, 무료)

```javascript
async function translate(text, from, to) {
  // 1. 로컬 캐시
  const cached = localStorage.getItem(`tr_${from}_${to}_${text}`);
  if (cached) return cached;
  
  // 2. CGO Voice DB (GitHub Pages)
  const url = `https://gh951.github.io/cgo-voice-db/dict/${from}_${to}.json`;
  try {
    const dict = await fetch(url).then(r => r.json());
    if (dict[text]) {
      localStorage.setItem(`tr_${from}_${to}_${text}`, dict[text]);
      return dict[text];
    }
  } catch (e) {}
  
  // 3. AI API 폴백 (Groq)
  return await aiTranslate(text, from, to);
}
```

## 📊 특허 연동

- **특허 #35**: 4단계 매칭 선번역 사전
- **특허 #36**: 경량 클라이언트 분산 저장
- **특허 #37**: GitHub Pages 무서버 공용 저장소
- **특허 #40**: 자기학습 분산 캐시 (역규모 경제)

## 🏗️ 연결 앱

- **CGO MESSAGE**: https://www.cgo-message.com/
- **CGO FULI**: https://www.c-go-fuli.com/

## 📝 기여

새 표현 추가는 `dict/*.json` PR로.

---

**Created**: 2026.04
**Version**: v1.0 (100 core phrases × 196 pairs)
**License**: Proprietary (MUFE Patent 10-2026-0060113)
