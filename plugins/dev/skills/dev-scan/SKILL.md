---
name: dev-scan
description: 개발 커뮤니티에서 기술 주제에 대한 다양한 의견 수집. "개발자 반응", "커뮤니티 의견", "developer reactions" 요청에 사용. Reddit, HN, Dev.to, Lobsters 등 종합.
version: 1.0.0
---

# Dev Opinions Scan

여러 개발 커뮤니티에서 특정 주제에 대한 다양한 의견을 수집하여 종합.

## Purpose

기술 주제에 대한 **다양한 시각**을 빠르게 파악:
- 찬반 의견 분포
- 실무자들의 경험담
- 숨겨진 우려사항이나 장점
- 커뮤니티별 온도 차이

## Data Sources

| Platform | Method |
|----------|--------|
| Reddit | Gemini CLI |
| Hacker News | WebSearch |
| Dev.to | WebSearch |
| Lobsters | WebSearch |

## Execution

### Step 1: Topic Extraction
사용자 요청에서 핵심 주제 추출.

예시:
- "React 19에 대한 개발자들 반응" → `React 19`
- "Bun vs Deno 커뮤니티 의견" → `Bun vs Deno`

### Step 2: Parallel Search (Single Message, 4 Sources)

**Reddit** (Gemini CLI - WebFetch blocked):
```bash
# 병렬로 3개 쿼리 실행 (주제에 맞게 쿼리 구성)
gemini -p "{일반 검색: topic + site:reddit.com}" &
gemini -p "{관련 서브레딧 2-3개 + topic}" &
gemini -p "{다른 각도의 관련 서브레딧 + topic + opinions/thoughts}" &
wait
```

쿼리 구성 가이드:
- 첫 번째: 일반 Reddit 검색
- 두 번째: 주제에 가장 관련된 서브레딧들 (예: React → r/reactjs r/webdev)
- 세 번째: 시니어/경험자 관점 서브레딧 (예: r/ExperiencedDevs) 또는 다른 관련 커뮤니티

**Other Sources** (WebSearch, parallel):
```
WebSearch: "{topic} site:news.ycombinator.com"
WebSearch: "{topic} site:dev.to"
WebSearch: "{topic} site:lobste.rs"
```

**CRITICAL**: 4개 검색을 반드시 **하나의 메시지**에서 병렬로 실행.

### Step 3: Synthesize & Present

수집된 데이터를 분석하여 의미 있는 인사이트를 도출한다.

#### 3-1. 의견 분류 및 패턴 파악

각 소스에서 수집된 의견들을 다음 기준으로 분류:

- **찬성/긍정**: 해당 기술/도구를 지지하는 의견
- **반대/부정**: 우려, 비판, 대안 제시
- **중립/조건부**: "~한 경우에만", "~와 함께 쓰면" 등의 조건부 의견
- **경험 기반**: 실제 프로덕션 사용 경험을 바탕으로 한 의견

#### 3-2. 공통 의견(Consensus) 도출

여러 커뮤니티에서 **반복적으로 등장하는** 의견을 식별:

- 2개 이상의 소스에서 동일한 포인트가 언급되면 공통 의견으로 분류
- 특히 Reddit과 HN에서 동시에 언급되는 의견은 신뢰도 높음
- 구체적인 수치나 사례가 포함된 의견 우선

#### 3-3. 논쟁점(Controversy) 식별

커뮤니티 간 또는 커뮤니티 내에서 **의견이 갈리는** 지점 파악:

- 같은 주제에 대해 상반된 의견이 존재하는 경우
- 댓글에서 활발한 토론이 벌어진 스레드
- "depends on...", "but actually..." 등의 반론이 많은 주제

#### 3-4. 주목할 시각(Notable Perspective) 선별

독특하거나 깊이 있는 인사이트 발굴:

- 다수 의견과 다르지만 논리적 근거가 탄탄한 의견
- 시니어 개발자나 해당 분야 전문가의 의견
- 실제 대규모 프로젝트 경험에서 나온 인사이트
- 다른 사람들이 놓치기 쉬운 엣지 케이스나 장기적 관점

#### 3-5. 커뮤니티별 온도 차이 정리

각 플랫폼의 전반적인 분위기 요약:

- Reddit: 전반적으로 긍정적/부정적/혼재?
- HN: 기술적 깊이 있는 논의가 있었나?
- Dev.to: 입문자 관점에서 어떤 반응?
- Lobsters: 시니어들의 시각은?

## Output Format

```markdown

## Key Insights

**Consensus (공통 의견)**:
- ...

**Controversy (논쟁점)**:
- ...

**Notable Perspective (주목할 시각)**:
- ...

---

## Sources
- [링크 목록...]
```

## Error Handling

| 상황 | 대응 |
|------|------|
| 검색 결과 없음 | 해당 플랫폼 생략, 다른 소스에 집중 |
| Gemini CLI 실패 | Reddit 생략하고 나머지 3개로 진행 |
| 주제가 너무 새로움 | 결과 부족 안내, 관련 키워드 제안 |

## Examples

**단순 주제**:
```
User: "Tailwind v4 개발자들 반응 어때?"
→ topic: "Tailwind v4"
→ 4개 소스 병렬 검색
→ 종합 인사이트 제공
```

**비교 주제**:
```
User: "pnpm vs yarn vs npm 커뮤니티 의견"
→ topic: "pnpm vs yarn vs npm comparison"
→ 4개 소스 병렬 검색
→ 각 도구별 선호도 정리
```

**논쟁적 주제**:
```
User: "Claude Code Plugin 에 대한 개발자들 생각"
→ topic: "Claude Code Plugin tips"
→ 4개 소스 병렬 검색
→ 종합 인사이트 제공
```
