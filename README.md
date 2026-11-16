# mini-dbms

C++17로 직접 만드는 미니 DBMS. 크래프톤 정글 미니 프로젝트.

## 목차
1. 무엇을 만드나
2. 진행 상황
3. 빌드와 실행
4. 문서

## 1. 무엇을 만드나

- **Phase 1**: SQL 처리기. `.sql` 파일의 `INSERT`/`SELECT`를 CLI로 실행하고, CRC32 프레임 단위의 append-only 바이너리 파일에 저장한다.
- **Phase 2**: 메모리 B+ 트리 인덱스(`id → 레코드 오프셋`), `EXPLAIN`, 100만 건 인덱스 조회 vs 전체 스캔 비교.
- **Phase 3**: HTTP API 서버. 직접 만든 스레드 풀, 원자적 INSERT 배치, NDJSON 스트리밍 SELECT.

설계의 중심은 크래시 일관성(프레임이 전부 남거나 전부 사라짐), 행 단위 스트리밍(결과 크기와 무관한 메모리), 락이 `Table` 안에만 있는 구조다.

## 2. 진행 상황

설계 완료, 구현 시작 전. 마일스톤은 `docs/architecture.md` §17.

## 3. 빌드와 실행

Docker 개발 컨테이너에서 빌드한다.

```bash
docker compose run --rm dev
cmake --preset debug && cmake --build --preset debug && ctest --preset debug
```

## 4. 문서

- `docs/architecture.md`: 설계 (단일 문서)
- `docs/decisions.md`: 결정 로그
- `docs/assignment.md`: 과제 원문
- `docs/refactoring.md`: 리팩터링 후보
