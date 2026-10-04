# ci-templates

Переиспользуемые workflow GitHub Actions.

## .github/workflows/java-maven-docker.yml

Reusable workflow (`on: workflow_call`) для Maven-приложения с Dockerfile:

```
build ──┐
        ├──> package (docker build + push в ghcr.io/<owner>/<repo>)
test  ──┘
```

### Подключение

```yaml
jobs:
  ci:
    uses: PavlovaAlexandra/ci-templates/.github/workflows/java-maven-docker.yml@main
    permissions:
      contents: read
      packages: write
```

### Входные параметры

| Параметр | По умолчанию | Описание |
|---|---|---|
| `runner` | `ubuntu-latest` | `self-hosted` для своего раннера |
| `java-version` | `21` | |
| `working-directory` | `.` | каталог с pom.xml и Dockerfile |
| `push-image` | `true` | `false`: только собрать образ |

Требования к проекту: Maven Wrapper (`./mvnw`) в репозитории, jar собирается в `target/`, Dockerfile копирует его оттуда.

### Доступ из приватного репозитория

Если `ci-templates` приватный: Settings → Actions → General → Access →
"Accessible from repositories owned by the user".
