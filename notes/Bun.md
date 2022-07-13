---
tags: js ts runtime yarn nodejs
---

# Bun

## JavaScriptCore 기반의 빠른 JavaScript 런타임/트랜스파일러/NPM 클라이언트

- Node, Deno와 같은 JavaScript 런타임
- 속도를 우선으로 개발
- `npm run`을 `bun run`으로 바꾸기만 해도 30배 빠르게 동작: https://twitter.com/jarredsumner/status/1454218996983623685
- npm과 호환 가능한 패키지 매니저를 포함
- `yarn`을 `bun install`로 바꾸기만 해도 20배 빠르게 패키지 설치 가능:
- WebKit에서 사용하는 JavaScriptCore을 확장하여 개발
- 시작 속도가 기존의 V8 등과 비교해서 월등히 빠름: https://twitter.com/jarredsumner/status/1499225725492076544
- 기존에 돌리던 JavaScript/TypeScript 앱을 그대로 쓸 수 있도록 설계: N-API, fs, path, Buffer 등을 포함한 여러 node.js API 및 fetch, WebSocket, ReadableStream 등을 포함한 Web API를 네이티브로 구현
- Node.js의 모듈 resolution 알고리즘을 구현하여 node_modules 사용 가능. ESM 및 CommonJS를 모두 지원. 내부적으로는 ESM을 사용.
- 모든 파일이 트랜스파일 되기 때문에 TypeScript 및 JSX를 모두 지원.
- `.env` 파일로부터 환경 변수를 알아서 불러오기 때문에 더 이상 `require('dotenv').load()`를 쓸 필요가 없음.

> ref. 
> - https://news.hada.io/topic?id=6921
> - https://bun.sh
