# 시작하기

이 가이드에서는 MKDocs 프로젝트를 처음부터 설정하고 GitHub Pages에 배포하는 과정을 단계별로 안내합니다.

## 📋 사전 요구사항

- [Python 3.8 이상](https://www.python.org/downloads/)
- [Git](https://git-scm.com/downloads)
- GitHub 계정

## 🛠️ 설치 과정

### 1. MKDocs 설치

```bash
# MKDocs 설치
pip install mkdocs

# Material 테마 설치
pip install mkdocs-material

# GitHub Pages 배포를 위한 ghp-import 설치
pip install ghp-import
```

### 2. 프로젝트 초기화

```bash
# 프로젝트 디렉토리로 이동
cd test

# MKDocs 프로젝트 초기화 (이미 완료됨)
# mkdocs new .
```

### 3. 로컬 서버 실행

```bash
# 로컬에서 문서 미리보기
mkdocs serve
```

이제 브라우저에서 `http://127.0.0.1:8000`으로 이동하면 문서 사이트를 확인할 수 있습니다.

## 📝 문서 작성

### Markdown 파일 생성

`docs/` 디렉토리 안에 `.md` 확장자를 가진 파일을 생성합니다:

```bash
# 새 문서 생성
touch docs/my-document.md
```

### 기본 Markdown 문법

```markdown
# 큰 제목
## 중간 제목
### 작은 제목

**굵게 표시**
*기울임꼴*

- 리스트 항목 1
- 리스트 항목 2

```python
# 코드 블록
def hello_world():
    print("Hello, World!")
```

> 인용구
```

## 🚀 GitHub Pages에 배포

### 1. GitHub 저장소 설정

1. GitHub에서 `test` 저장소 생성
2. 로컬 저장소를 원격 저장소에 연결

```bash
git remote add origin https://github.com/sechuh-pixel/test.git
git branch -M main
git push -u origin main
```

### 2. GitHub Pages 활성화

1. GitHub 저장소로 이동
2. `Settings` → `Pages` 메뉴 선택
3. `Source`에서 `Deploy from a branch` 선택
4. `Branch`에서 `gh-pages` 선택
5. `Save` 클릭

### 3. 자동 배포

```bash
# GitHub Pages에 배포
mkdocs gh-deploy
```

이 명령어는 자동으로 `gh-pages` 브랜치를 생성하고 빌드된 사이트를 업로드합니다.

## 🤖 CI/CD 자동화

### GitHub Actions 워크플로우

`.github/workflows/deploy.yml` 파일을 생성하여 자동 배포를 설정합니다.

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

이제 `main` 브랜치에 푸시할 때마다 자동으로 GitHub Pages에 배포됩니다.

## 📚 다음 단계

- [문서 작성 가이드](guide.md)에서 더 자세한 Markdown 사용법을 배워보세요
- [API Reference](api.md)에서 MKDocs의 모든 기능을 확인해보세요