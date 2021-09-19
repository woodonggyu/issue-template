# Github 활용한 프로젝트 관리

우리가 어떠한 목표를 가지고 프로젝트를 진행할 때, 성공적으로 프로젝트를 완료하기 위해서는 관리 계획을 수립하고, 이를 체계적으로 수행해나가는 것이 중요하다.

소프트웨어 개발 프로젝트에서도 성공적인 프로젝트 완료를 위한 여러 가지 소프트웨어 개발 방법론을 두고 효율적인 방법론을 사용하는 경우가 많다.

프로젝트 관리는 어떤 도움을 주는가?

1. **가시성** : 프로젝트 진행 상황을 포함한 전반적인 작업을 쉽게 파악할 수 있다.

2. **명확성** : 역할이 명확하게 정의되어, 의사결정 프로세스 개선 및 책임을 보장할 수 있다.

3. **효율성** : 프로젝트 시작 단계를 가속화하고 전체 프로젝트 일정 및 예산을 줄일 수 있다.

<br>

Github 에서는 개인 프로젝트와 협업 시에 유용한 여러 가지 기능을 지원하며, 이러한 기능을 사용하여 일정, 이슈 및 기능 등에서의 관리 효율성을 얻을 수 있다.

<br>

## Issue Template 생성

소스 코드와 관련된 신규 기능 개발 작업이나 버그가 있을 때 관련 작업을 요청하거나 수정을 진행하기 위한 목적으로 이슈를 생성한다. 만약, 이슈를 생성하는 누군가가 "해당 기능이 되지 않아요~" 라고만 한다면 이슈를 파악하고 완료되기까지 많은 시간이 소요된다.

그렇기에 **`Issue Template`** 을 통해 이슈를 구분하고 (ex. Bug Report, Feature Request 등) 지정된 템플릿을 사용하여 정형화된 형식으로 내용을 작성할 수 있도록 도움을 준다. 

담당자 입장에서도 요구사항(또는 문제사항)을 정확하게 파악하고, 해당 이슈를 신속하게 대응할 수 있다는 측면에서 유용하다.

* [Configuring issue templates for your repository](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository)

<br>

생성한 이슈 템플릿은 `.github/ISSUE_TEMPLATE` 디렉토리에 생성된다. [[참고]](https://github.com/woodonggyu/issue-template/tree/master/.github/ISSUE_TEMPLATE)

프로젝트별로 각각의 이슈 템플릿을 매번 직접 생성하는 것보다, 이슈 성격(ex. Backend, Frontend, Security 등) 별로 템플릿을 생성한 후 이를 해당 레파지토리에 적용하면 편리하게 사용할 수 있다.

<br>

## Label Template 생성
Issue Template 또는 Pull Request 시, 해당 내용에 적합한 라벨을 적용함으로써 이슈별 검색 또는 분류를 통해 관리 및 활용 효율성을 높일 수 있다.

GitHub 에서 수동으로 생성 방법은 다음과 같다.

1. Label 을 생성하고자 하는 레파지토리로 이동
2. Issues > 🏷 Labels > New label
3. Label 생성

<br>

위와 같이 수동으로 생성할 경우, 레파지토리 마다 이를 적용해야하는 번거로움이 생긴다.
`github-label-sync` 라이브러리를 통해 GitHub Label 을 동기화할 수 있다.

<br>

1. **`github-label-sync` 라이브러리 설치**

```
# sudo npm install -g github-label-sync
```

2. **GitHub 개인 액세스 토큰 생성 [[참고]](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token)**

3. **Label 정의 [[참고]](https://github.com/woodonggyu/issue-template/blob/master/.github/labels.json)**

4. **레파지토리 Label 적용**

```
# sudo github-label-sync --access-token [액세스 토큰] --labels labels.json [계정명]/[저장소 이름]
```

<br>

## Pull Request Template 생성

`Pull Request (이하 PR)` 는 **"해당 프로젝트의 소스에 기여한 내용이 있으니 작업한 내용을 검토하고 합쳐주세요" 의미를 가지고 있다.** 어떤 상황에서 Pull Request 가 필요할까?

* 특정 프로젝트의 작업한 내용에 대한 커밋 또는 푸쉬 권한이 없을 경우

* 조직 내에서 작업한 내용을 master 브랜치에 병합(Merge) 시, 코드 리뷰 등 검토가 필요한 경우

<br>

우리는 `Pull Request Template` 을 정의함으로써, 정형화된 형식으로 어떤 브랜치에서 어떤 작업을 했는지 등 작업한 내용에 대해 간결하게 전달할 수 있다.

* [Creating a pull request template for your repository](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository)

<br>

생성한 이슈 템플릿은 `.github/ISSUE_TEMPLATE/PULL_REQUEST_TEMPLATE.md` 또는 `.github/PULL_REQUEST_TEMPLATE.md` 에 생성된다. [[참고]](https://github.com/woodonggyu/issue-template/tree/master/.github/PULL_REQUEST_TEMPLATE)

위 경로의 차이점은 단일 템플릿 또는 다수 템플릿에 따라 다르다. 
여러 템플릿을 사용할 경우, ISSUE_TEMPLATE 디렉토리 내 템플릿을 작성한다.

<br>

## ZenHub 연동

GitHub 에서 프로젝트를 진행하다보면, 수 많은 이슈로 인해 이슈 관리가 어려워진다. Label Template 을 통해 이슈 관리를 진행할 수 있지만, GitHuB 에서 제공해주는 UI 에서는 이를 한 눈에 보기 어렵다.

**`ZenHub` 는 이슈를 칸반 보드 형태로 제공해주는 플러그인이다.** 개인의 경우 무료로 사용 가능하다.

설치 방법은 Google 검색 시, 간단하게 연동 방법을 설명하기에 생략한다. 사용 방법은 [링크](https://help.zenhub.com/support/home)를 참조한다.

![](https://images.velog.io/images/woodonggyu/post/1cf421d2-96b0-460b-868c-f7edc45d17fe/image.png)
