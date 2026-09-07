# 스타트·엔드 카메라 점프 프롬프트

스타트·엔드 이미지 두 장을 비교하고, 사용자에게 시간과 이동 방식을 질문한 뒤 영상 생성용 영어 프롬프트를 작성하는 Codex 스킬입니다. 영상을 직접 생성하지는 않습니다.

현재 버전: **v1.1.0**

## 사용 흐름

이미지 두 장 첨부 → 구도 확인 → 생성 길이·이동 완료 시점·이동 방식 선택 → 복사용 프롬프트 작성.

- 이동 방식: 직진 / 지정 지점으로 이동 / 제자리 방향 전환 / 회전하며 진입.
- 회전은 왼쪽·오른쪽을 선택합니다.
- 제자리 방향 전환은 위치를 유지하고 시선만 회전합니다.
- 회전하며 진입은 방향 전환과 위치 이동을 함께 수행합니다.
- 기본 제안은 3초 생성, 1초 이내 이동 완료, 이후 엔드 구도 정지입니다. 사용자 답변을 받은 뒤 확정합니다.
- 짧은 블러를 동반한 스냅과 즉시 정지를 유지합니다. 구체적인 시간 지시 준수 여부는 생성 결과로 확인해야 합니다.

호출 예시:

```text
$start-end-camera-jump-ko
이미지 1은 스타트, 이미지 2는 엔드야.
두 이미지를 확인하고 영상 길이와 이동 방식을 먼저 물어봐줘.
```

## 처음 설치하는 사람

Codex에 다음 문장을 전달하세요.

```text
https://github.com/ddokkang2/start-end-camera-jump-ko
이 저장소의 v1.1.0 태그를 Codex 사용자 스킬로 설치해줘.
스킬 이름은 start-end-camera-jump-ko이고, SKILL.md는 저장소 루트에 있어.
```

기본 설치 위치는 `~/.codex/skills/start-end-camera-jump-ko`입니다. `CODEX_HOME`을 따로 설정했다면 해당 경로의 `skills` 폴더를 사용합니다. 설치 후 다음 턴에서 호출하고, 현재 목록에 보이지 않으면 새 대화에서 호출하세요.

## 기존 사용자 업데이트

GitHub에 푸시해도 기존 로컬 설치 파일이 자동으로 바뀌지는 않습니다. 다음 문장을 Codex에 전달하세요.

```text
설치된 start-end-camera-jump-ko 스킬을
https://github.com/ddokkang2/start-end-camera-jump-ko 의 v1.1.0으로 업데이트해줘.
현재 설치 경로와 버전을 확인하고, 기존 폴더는 스킬 검색 경로 밖에 백업해줘.
사용자 수정 사항이 있으면 덮어쓰기 전에 차이를 알려줘.
해당 태그의 스킬 파일로 교체한 뒤 metadata.version이 1.1.0인지 확인하고,
SKILL.md, agents/openai.yaml, references/success-patterns.md가 원격 버전과 일치하는지 검증해줘.
```

### ZIP으로 직접 설치한 경우

1. [v1.1.0 ZIP](https://github.com/ddokkang2/start-end-camera-jump-ko/archive/refs/tags/v1.1.0.zip)을 다운로드해 압축을 풉니다.
2. 기존 설치 폴더를 스킬 검색 경로 밖에 백업합니다. 직접 수정한 내용이 있으면 새 파일과 비교합니다.
3. 기존 설치 폴더를 새 버전으로 교체합니다. `start-end-camera-jump-ko/SKILL.md`가 바로 존재해야 하며 압축 폴더를 한 단계 더 중첩하지 않습니다.
4. `SKILL.md`의 `metadata.version`이 `1.1.0`인지 확인합니다.

### 설치 폴더가 Git clone인 경우

먼저 해당 폴더의 `git remote -v`가 이 저장소를 가리키는지 확인하고 `git status --short`로 직접 수정한 파일이 없는지 확인하세요. 수정 사항이 있으면 먼저 백업·정리하세요.

최신 `main`을 추적하는 설치는 설치 폴더에서 다음을 실행합니다.

```sh
git switch main
git pull --ff-only origin main
```

특정 릴리스 v1.1.0에 고정하려면 다음을 실행합니다. 이 경우 detached HEAD 상태가 되는 것이 정상입니다.

```sh
git fetch origin tag v1.1.0
git switch --detach v1.1.0
```

일반 파일 복사 방식으로 설치했다면 `git pull`을 사용할 수 없으므로 위의 Codex 요청문 또는 ZIP 교체 방식을 사용하세요. 일반 설치 도구는 기존 폴더가 있으면 중단할 수 있으므로 업데이트는 백업 후 교체해야 합니다.

## 변경 이력

[CHANGELOG.md](CHANGELOG.md)를 참고하세요.
