# 1. Vue CLI를 사용한 TypeScript 프로젝트 생성

Vue CLI는 Vue 프로젝트를 쉽게 설정하고 관리할 수 있는 도구

TypeScript를 사용하려면 다음 명령어로 프로젝트를 생성할 수 있다

```bash

vue create my-project
cd my-project
vue add typescript

```

이 명령어는 프로젝트를 생성하고 TypeScript를 추가하는 Vue CLI 플러그인을 설치

# 2. 기존 프로젝트에 TypeScript 추가

이미 생성된 Vue 프로젝트에 TypeScript를 추가하려면 다음 명령어를 사용할 수 있다

```bash

vue add typescript

```

이 명령어는 TypeScript 관련 의존성을 설치하고, tsconfig.json 파일을 생성하여 TypeScript 설정을 추가

# 3. 수동으로 설정

수동으로 TypeScript를 설정하려면 다음 단계를 따를 수 있음

### 3.1 TypeScript 및 관련 패키지 설치

```bash
npm install --save-dev typescript ts-loader

```

### 3.2 tsconfig.json 파일 생성

프로젝트 루트 디렉토리에 tsconfig.json 파일을 생성하고 필요한 TypeScript 설정을 추가

```json
{
  "compilerOptions": {
    "target": "esnext",
    "module": "esnext",
    "moduleResolution": "node",
    "strict": true,
    "jsx": "preserve",
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "allowSyntheticDefaultImports": true,
    "strictPropertyInitialization": false
  },
  "include": [
    "src/**/*.ts",
    "src/**/*.d.ts",
    "src/**/*.tsx",
    "tests/**/*.ts",
    "tests/**/*.tsx",
    "typings/**/*.d.ts",
    "shims-tsx.d.ts",
    "shims-vue.d.ts"
  ],
  "exclude": ["node_modules"]
}
```

### 3.3 확장자 매핑 설정

src 폴더에 shims-vue.d.ts와 shims-tsx.d.ts 파일을 생성하고 다음과 같이 설정

- shims-vue.d.ts

```typescript
declare module "*.vue" {
  import Vue from "vue";
  export default Vue;
}
```

- shims-tsx.d.ts

```typescript
import Vue, { VNode } from "vue";

declare global {
  namespace JSX {
    interface Element extends VNode {}
    interface ElementClass extends Vue {}
    interface IntrinsicElements {
      [elem: string]: any;
    }
  }
}
```

이렇게 하면 Vue.js 프로젝트에 TypeScript를 수동으로 설정가능

두 번째와 세 번째 방법에서는 수동으로 설정하는 방식이 있으며, 세 번째 방법은 더욱 세밀한 제어를 제공
