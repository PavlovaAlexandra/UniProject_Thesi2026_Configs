# ci-templates

Переиспользуемые шаблоны GitLab CI.

## templates/java-maven-docker.gitlab-ci.yml

Базовый пайплайн для Maven-приложения с Dockerfile:

```
build ──┐
        ├──> package (Kaniko -> $CI_REGISTRY_IMAGE)
test  ──┘
```

### Подключение

```yaml
include:
  - project: "$CI_PROJECT_NAMESPACE/ci-templates"
    ref: main
    file: "/templates/java-maven-docker.gitlab-ci.yml"
```

### Переменные (можно переопределить в проекте)

| Переменная | По умолчанию |
|---|---|
| `MAVEN_IMAGE` | `maven:3.9-eclipse-temurin-21` |
| `KANIKO_IMAGE` | `gcr.io/kaniko-project/executor:v1.23.2-debug` |
| `DOCKERFILE_PATH` | `Dockerfile` |
| `IMAGE_NAME` | `$CI_REGISTRY_IMAGE` |
| `IMAGE_TAG` | `$CI_COMMIT_SHORT_SHA` |
| `KANIKO_EXTRA_ARGS` | пусто (например `--insecure` для HTTP-registry) |

Требования к проекту: сборка кладёт jar в `target/`, Dockerfile копирует его оттуда.
