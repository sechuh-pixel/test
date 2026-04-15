# API Reference

이 섹션에서는 MKDocs와 Material for MKDocs에서 사용할 수 있는 주요 API와 설정 옵션들을 상세히 설명합니다.

## 📋 MKDocs 설정 (mkdocs.yml)

### 기본 설정

```yaml
site_name: 사이트 이름
site_description: 사이트 설명
site_author: 작성자 이름
site_url: https://example.com
repo_url: https://github.com/user/repo
repo_name: user/repo
```

### 테마 설정

```yaml
theme:
  name: material
  language: ko
  palette:
    primary: indigo
    accent: indigo
  features:
    - navigation.tabs
    - navigation.sections
    - navigation.expand
    - navigation.indexes
    - search.suggest
    - search.highlight
    - content.tabs.link
    - content.code.annotation
    - content.code.copy
```

### 네비게이션 설정

```yaml
nav:
  - Home: index.md
  - Getting Started: getting-started.md
  - Guide:
    - Basic: guide.md
    - Advanced: guide/advanced.md
  - API Reference: api.md
```

### 마크다운 확장

```yaml
markdown_extensions:
  - admonition
  - attr_list
  - md_in_html
  - toc:
      permalink: true
  - pymdownx.arithmatex:
      generic: true
  - pymdownx.betterem:
      smart_enable: all
  - pymdownx.caret
  - pymdownx.details
  - pymdownx.emoji:
      emoji_generator: !!python/name:material.extensions.emoji.to_svg
      emoji_index: !!python/name:material.extensions.emoji.twemoji
  - pymdownx.highlight:
      anchor_linenums: true
  - pymdownx.inlinehilite
  - pymdownx.keys
  - pymdownx.magiclink:
      repo_url_shorthand: true
      user: squidfunk
      repo: mkdocs-material
  - pymdownx.mark
  - pymdownx.smartsymbols
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:pymdownx.superfences.fence_code_format
  - pymdownx.tabbed:
      alternate_style: true
  - pymdownx.tasklist:
      custom_checkbox: true
  - pymdownx.tilde
```

## 🎨 Material 테마 옵션

### 색상 팔레트

```yaml
theme:
  palette:
    primary: red | pink | purple | deep-purple | indigo | blue | light-blue | cyan | teal | green | light-green | lime | yellow | amber | orange | deep-orange | brown | grey | blue-grey
    accent: red | pink | purple | deep-purple | indigo | blue | light-blue | cyan | teal | green | light-green | lime | yellow | amber | orange | deep-orange
```

### 레이아웃 옵션

```yaml
theme:
  features:
    - navigation.tabs
    - navigation.tabs.sticky
    - navigation.sections
    - navigation.expand
    - navigation.indexes
    - navigation.top
    - search.highlight
    - search.share
    - search.suggest
    - toc.integrate
    - header.autohide
    - navigation.sections
    - navigation.tabs
    - navigation.tabs.sticky
    - navigation.sections
    - navigation.expand
    - navigation.indexes
    - navigation.top
    - search.highlight
    - search.share
    - search.suggest
    - toc.integrate
    - header.autohide
```

### 사이드바 설정

```yaml
theme:
  features:
    - navigation.sections
    - navigation.expand
    - navigation.indexes
```

## 🔧 명령어

### mkdocs 명령어

```bash
# 새 프로젝트 생성
mkdocs new [프로젝트명]

# 로컬 서버 실행
mkdocs serve

# 사이트 빌드
mkdocs build

# GitHub Pages에 배포
mkdocs gh-deploy

# 설정 파일 검증
mkdocs config

# 파일 감시 모드
mkdocs serve --watch-theme
```

### mkdocs serve 옵션

```bash
mkdocs serve [OPTIONS]

Options:
  -a, --dev-addr <IP:PORT>  IP 주소와 포트 지정
  -s, --strict              오류 발생 시 서버 중지
  -t, --theme <NAME>        테마 이름 지정
  -f, --config-file <FILE>  설정 파일 경로 지정
  -d, --docs-dir <PATH>     문서 디렉토리 경로 지정
  -e, --site-dir <PATH>     사이트 디렉토리 경로 지정
  -q, --quiet               출력 최소화
  -v, --verbose             상세 출력
```

### mkdocs build 옵션

```bash
mkdocs build [OPTIONS]

Options:
  -c, --clean               빌드 전 기존 파일 삭제
  -f, --config-file <FILE>  설정 파일 경로 지정
  -d, --docs-dir <PATH>     문서 디렉토리 경로 지정
  -e, --site-dir <PATH>     사이트 디렉토리 경로 지정
  -q, --quiet               출력 최소화
  -v, --verbose             상세 출력
  -w, --watch               파일 변경 감시
```

## 📦 플러그인

### 인기 있는 MKDocs 플러그인

```yaml
plugins:
  - search
  - awesome-links
  - git-revision-date-localized
  - git-authors
  - minify:
      minify_html: true
  - awesome-pages
```

### 플러그인 설치

```bash
# 검색 플러그인
pip install mkdocs-search

# Git 정보 플러그인
pip install mkdocs-git-revision-date-localized-plugin

# 페이지 정리 플러그인
pip install mkdocs-awesome-pages-plugin

# HTML 최소화 플러그인
pip install mkdocs-minify-plugin
```

## 🌐 GitHub Actions 워크플로우

### 기본 배포 워크플로우

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      
      - name: Install dependencies
        run: |
          pip install mkdocs
          pip install mkdocs-material
          pip install ghp-import
      
      - name: Deploy to GitHub Pages
        run: |
          mkdocs gh-deploy --force
```

### 고급 워크플로우

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  groups:
    deploy-pages:
      cancel-in-progress: true
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      
      - name: Install dependencies
        run: |
          pip install mkdocs
          pip install mkdocs-material
          pip install ghp-import
      
      - name: Build site
        run: mkdocs build
      
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2
        with:
          path: site

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
```

## 📊 성능 최적화

### 빌드 최적화

```yaml
# mkdocs.yml
site_name: My Site

# 빌드 옵션
use_directory_urls: true
strict: true
dev_addr: 127.0.0.1:8000

# 파일 무시
watch:
  - '!node_modules'
  - '!*.log'
```

### 캐싱 전략

```yaml
# mkdocs.yml
plugins:
  - minify:
      minify_html: true
      minify_js: true
      minify_css: true
```

## 🔍 검색 최적화

### 검색 설정

```yaml
# mkdocs.yml
plugins:
  - search:
      lang: ko
      separator: '[\s\-\.]+'
      prebuild_index: true
```

### 검색어 가이드

```markdown
<!-- 검색어 가이드 추가 -->
<meta name="description" content="검색에 포함될 설명">
<meta name="keywords" content="검색어1, 검색어2, 검색어3">
```

이 API Reference는 MKDocs 프로젝트를 보다 효율적으로 관리하고 최적화하는 데 도움이 됩니다. 자세한 내용은 [공식 문서](https://www.mkdocs.org/user-guide/configuration/)를 참고하세요.