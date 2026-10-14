# Codex에서 Paper2Assets와 Paper2Poster 검색하기

공식 문서: https://developers.openai.com/codex/skills/

Codex는 시작 작업 디렉터리(CWD)에서 Git 저장소 루트까지 각 디렉터리의
`.agents/skills`를 검색하며, Skill 디렉터리의 심볼릭 링크도 지원합니다.
저장소의 `.codex/skills` 연결만으로 공식 검색 경로 등록을 대신하지 않습니다.

이 저장소는 원본 파일을 복사하거나 수정하지 않고 다음 상대 경로 연결을 제공합니다.

```text
.agents/skills/paper2assets -> ../../ResearchStudio-Reel/skills/paper2assets
.agents/skills/paper2poster -> ../../ResearchStudio-Reel/skills/paper2poster
```

상대 경로와 Git에 저장된 연결을 사용하므로 저장소를 다른 위치에 체크아웃해도
동일한 저장소 구조에서는 연결이 유지됩니다. 기존 `.codex/skills`는 보존합니다.

## 새 클라우드 작업에서 확인

1. 이 변경사항을 포함하는 클라우드 환경 스냅샷을 저장·게시하거나, 이 커밋을
   포함하는 저장소 버전을 새 작업에 제공하세요. 로컬 Git 커밋 자체는 GitHub 푸시나
   게시된 클라우드 스냅샷 갱신을 의미하지 않습니다.
2. Codex의 시작 작업 디렉터리를 `/workspace/ResearchStudio` 또는 그 하위 디렉터리로
   지정하세요. `/workspace`에서 시작하면 하위 저장소의 `.agents/skills`는 위쪽 검색
   범위에 포함되지 않습니다. 실행 중 셸에서 `cd`만 하는 것과 새 세션의 시작 CWD를
   지정하는 것은 다릅니다.
3. 새 작업의 Skill 목록 또는 선택기에서 `paper2assets`, `paper2poster`를 확인하세요.
   목록을 사용할 수 없다면 에이전트에게 현재 사용 가능한 Skill의 name, description,
   SKILL.md 경로만 보고하도록 요청하세요. 실제 논문 처리나 포스터 생성은 요청하지 마세요.
4. 두 경로가 읽히는지 확인하세요.

```bash
cd /workspace/ResearchStudio
ls -l .agents/skills
head -n 5 .agents/skills/paper2assets/SKILL.md
head -n 5 .agents/skills/paper2poster/SKILL.md
```

5. 연결 파일이 보여도 자동 인식 확인은 별도로 필요합니다. 나타나지 않으면 시작 CWD,
   사용한 환경 버전 및 연결 대상을 확인하고 Codex를 재시작하세요. 지원하는 클라이언트에서는
   `$paper2assets`, `$paper2poster`로 명시적으로 참조할 수 있습니다. 점검 시에는
   메타데이터만 확인하라는 지시를 함께 주세요.

## 실행 도구

Skill 검색과 Python 실행환경 활성화는 별도입니다. 기존 클라우드 도구를 실행하려면:

```bash
cd /workspace/ResearchStudio
source /workspace/paper-tools/activate.sh
```

브라우저 기반 CLI의 기존 `with-system-chromium.py` 래퍼와 실행 권한 요건은
`/workspace/paper-tools/SETUP.md`를 따르세요. 이 연결 설정은 실제 논문 포스터를 생성하지 않습니다.
