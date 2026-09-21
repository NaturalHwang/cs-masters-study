# CS-MASTERS-FOUNDATIONS v2.1 — GitHub-backed scheduled generation

## Source of truth
- Repository: NaturalHwang/cs-masters-study
- Output directory: materials/
- Progress state: state/progress.json
- Fixed 1st-stage curriculum: Day01~Day60.
- Do not reorder, skip, or replace a Day unless the user explicitly changes the curriculum.
- Day01~Day60 order is fixed; explanation depth/examples/prerequisite recap may adapt.

## Learner and format
- Assume CS bachelor's coursework was taken but mostly forgotten.
- Korean prose with important English terms in parentheses.
- Main direction: Distributed Systems + Software Engineering.
- About 30 minutes per session.
- One central question per day.
- Structure each HTML with:
  1) 오늘의 주제
  2) 학습 목표 2~4개
  3) 이전 학습과의 연결
  4) 필요한 선수지식 + 3~5분 복습
  5) 문제 상황
  6) 핵심 개념(직관→예→정의→동작)
  7) 실제 시스템 사례
  8) Trade-off와 대안
  9) 간단한 심화
  10) 핵심 요약 ≤5
  11) 확인 질문 3~5개 + details/summary 접이식 해설
  12) 연구자의 관점
  13) Research Question 후보(2단계부터)
  14) 다음 학습 예고
  15) 참고자료와 지금 읽을 부분
- At least one question must be a 3~5 minute execution trace / counterexample / design comparison.
- Use a small inventory reservation service as the recurring example when useful.
- Prefer official docs, university material, original papers.
- Never invent performance numbers, papers, or learning history.

## Scheduling and progress rule
- Normal schedule: Asia/Seoul, Monday-Friday 09:00.
- Public holidays that fall on weekdays are included unless the user later changes this.
- Before generating, read state/progress.json.
- Generate exactly progress.next_day.
- Do NOT infer the next Day only from today's calendar date.
- If generation fails, keep progress.next_day unchanged.
- If generation and GitHub verification both succeed, update:
  - last_successful_day
  - next_day = last_successful_day + 1
  - last_successful_path
  - last_successful_commit if available
  - last_run_status = "success"
- User reading/completion/understanding remain unknown unless explicitly provided.
- Never treat file generation as learning completion.

## GitHub output contract
1. Build complete self-contained UTF-8 HTML in memory.
2. Path: materials/YYYY-MM-DD_DayNN_주제.html using the curriculum's canonical date for that Day.
3. If the path does not exist, create_file.
4. If it exists and regeneration is intended, fetch current SHA then update_file.
5. After write success, fetch_file from main and verify:
   - correct Day number
   - correct topic
   - all 15 sections
   - understanding questions and collapsible explanations
6. Only after verification update state/progress.json.
7. On any connector/write/verification failure:
   - do not dump the lesson body into chat
   - report only Day/topic, failed stage, and short available error
   - do not advance next_day
8. On success, final message should be concise and include the GitHub file link.

## Accuracy guardrails
- Concurrency ≠ Parallelism.
- Atomicity ≠ Visibility.
- OS locks ≠ DB isolation.
- 2PL ≠ 2PC.
- ACID Consistency ≠ distributed consistency.
- TCP delivery semantics ≠ exactly-once business processing.
- Timeout is not proof of non-execution.
- MVCC alone does not imply serializability.
- Synchronous replication alone does not imply linearizability.
- Lamport: a→b implies L(a)<L(b), converse generally false.
- CAP concerns partition-time tension between linearizability-style consistency and availability, not “pick any two at all times.”
- Passing tests is not a proof of correctness.

## Fixed curriculum
### Week 1
- Day01 2026-09-14 — 컴퓨터에서 프로그램은 어떻게 실행되는가: CPU·Memory·Storage; Program vs Process; OS 역할
- Day02 2026-09-15 — 프로세스의 주소 공간과 격리: Address Space; Code/Data; Stack/Heap; Process Isolation
- Day03 2026-09-16 — 스레드와 실행 문맥: Process vs Thread; 공유 데이터; 개별 Stack·Register; Context Switching
- Day04 2026-09-17 — 동시성이 필요한 이유: Sequential/Concurrent/Parallel; 실행·준비·대기; Blocking I/O
- Day05 2026-09-18 — Week 1 복습: Program→Process→Thread→Memory→Concurrency; 실행 추적

### Week 2
- Day06 2026-09-21 — 경쟁 조건과 원자성: Race Condition; Read-Modify-Write; Atomicity; Invariant
- Day07 2026-09-22 — 임계 구역과 뮤텍스: Critical Section; Mutex/Lock; Mutual Exclusion; 잠금 범위
- Day08 2026-09-23 — 조건 변수: Condition Variable; Wait/Notify; 조건 재검사; Producer/Consumer
- Day09 2026-09-24 — 세마포어: Semaphore; Permit; Acquire/Release; Mutex·Condition Variable 비교
- Day10 2026-09-25 — Week 2 복습: 동기화 도구 선택; Deadlock 한 사례; 잠금 순서; Safety/Liveness

### Week 3
- Day11 2026-09-28 — 네트워크 통신 개요: Message; Byte; Protocol; 계층별 역할; Shared Memory vs Message Passing
- Day12 2026-09-29 — IP·패킷과 목적지: IP Address; Packet; Router; 손실·지연·재정렬
- Day13 2026-09-30 — TCP와 UDP의 계약: TCP Byte Stream; UDP Datagram; 순서·재전송
- Day14 2026-10-01 — Socket과 Client/Server: Port; Connect/Send/Receive; Serialization; 메시지 경계
- Day15 2026-10-02 — Week 3 복습: Thread→Socket→TCP/UDP→IP→Server; 대기 지점

### Week 4
- Day16 2026-10-05 — HTTP 요청·응답과 API 계약
- Day17 2026-10-06 — DNS와 캐시된 이름
- Day18 2026-10-07 — Latency·Bandwidth·Throughput와 병목
- Day19 2026-10-08 — Timeout·Retry와 Idempotency
- Day20 2026-10-09 — 1개월차 종합: 요청·성능·실패 추적; 요청 ID·로그; 평균 vs p95

### Week 5
- Day21 2026-10-12 — Database·Table·Key가 필요한 이유
- Day22 2026-10-13 — Memory·Storage와 Page 단위 접근
- Day23 2026-10-14 — Array·Binary Search·Big-O
- Day24 2026-10-15 — B+ Tree Index 원리
- Day25 2026-10-16 — Week 5 복습: Table→Page→Search Cost→Index

### Week 6
- Day26 2026-10-19 — Query 실행: Parse→Plan→Execute; Seq Scan vs Index Scan
- Day27 2026-10-20 — Buffer Pool·Cache·Dirty Page·Flush
- Day28 2026-10-21 — Transaction과 ACID
- Day29 2026-10-22 — Isolation과 Serializability
- Day30 2026-10-23 — Week 6 복습: Query/Buffer/Transaction

### Week 7
- Day31 2026-10-26 — Concurrency Control: Locking·MVCC·Snapshot
- Day32 2026-10-27 — Isolation Levels: Dirty/Nonrepeatable/Phantom; Read Committed 중심
- Day33 2026-10-28 — Write-Ahead Log
- Day34 2026-10-29 — Crash Recovery: REDO·Checkpoint; UNDO와 저장정책
- Day35 2026-10-30 — Week 7 복습: Lock/Isolation/MVCC/WAL 책임

### Week 8
- Day36 2026-11-02 — 좋은 소프트웨어와 검증 가능한 요구사항
- Day37 2026-11-03 — Abstraction·Interface·API Contract
- Day38 2026-11-04 — Modularity·Coupling·Cohesion
- Day39 2026-11-05 — Testing·Regression·Refactoring
- Day40 2026-11-06 — 2개월차 종합: 요구→설계→실행→저장→테스트; 로그; CI 최소 흐름

### Week 9
- Day41 2026-11-09 — Distributed System 정의: 독립 실행 주체·Message Passing·분산 상태
- Day42 2026-11-10 — Scalability·Availability·Fault Tolerance; Single Point of Failure
- Day43 2026-11-11 — Scale-up vs Scale-out; 상태 배치; Replication vs Sharding
- Day44 2026-11-12 — Partial Failure·Failure Model·Partition
- Day45 2026-11-13 — Week 9 복습: Failure Model; Safety vs Liveness

### Week 10
- Day46 2026-11-16 — 분산시스템에서 시간과 순서가 어려운 이유
- Day47 2026-11-17 — Physical Clock·Clock Drift·Monotonic Clock
- Day48 2026-11-18 — Causality·Happens-before·Partial vs Total Order
- Day49 2026-11-19 — Lamport Clock
- Day50 2026-11-20 — Week 10 복습: Physical/Monotonic/Logical Clock; 인과 그래프

### Week 11
- Day51 2026-11-23 — Replication 목적; Replica; Replication vs Backup
- Day52 2026-11-24 — Leader/Follower와 Replication Log
- Day53 2026-11-25 — Sync/Async Replication; ACK; 전송·영속화·적용
- Day54 2026-11-26 — Replication Lag·Stale Read·Read-your-writes
- Day55 2026-11-27 — Week 11 복습: Failover·Split Brain; 승인 데이터 소실; 3-node majority intersection

### Week 12
- Day56 2026-11-30 — Consistency Model; read/write History; ACID C와 구별
- Day57 2026-12-01 — Linearizability vs Eventual Consistency
- Day58 2026-12-02 — CAP Theorem의 범위
- Day59 2026-12-03 — Consensus 문제 정의; Agreement·Validity·Termination; Quorum 직관
- Day60 2026-12-04 — 기초과정 종합: 실행→동시성→통신→트랜잭션→복구→실패→시간→복제→일관성→합의

## Depth limits
- Day01~04: commands/variables/addresses/function calls first; no CPU/compiler/VM internals dump.
- Day06~10: small executions only: one variable, one queue, two locks.
- Day11~20: start from bytes/protocols; no full-layer memorization or TCP congestion-control implementation.
- Day21~27: Table/Key→Page→Array/Search/Big-O→Tree/Index→Query→Buffer.
- Day28~35: distinguish ACID goals, serializability, concurrency control, isolation, WAL, recovery.
- Day36~40: requirement/contract→change boundary→testing.
- Day41~45: distinguish scale, availability, partitioned state, partial failure.
- Day46~50: explain set/directed graph/transitivity/max only as needed; no Vector Clock detail yet.
- Day51~55: distinguish transfer, durability, apply, ACK.
- Day56~60: explain consistency with one-object read/write histories; detailed Raft/Paxos/2PC later.

## Stage 2
After Day60 review, move to deeper study beginning next normal weekday. Main flow:
- Distributed Systems: Consensus→Raft→Paxos→Fault Tolerance→Distributed Transaction/2PC→Distributed Storage/DB→Large-scale Systems; include BFT, Replication, Consistency, CAP, MVCC, Stream Processing, Cloud, Microservices as dependencies require.
- Software Engineering: Modularity, Architecture, API Design, Testing, Reliability, Observability, Maintainability, Evolution, Refactoring, Technical Debt, Requirements, Developer Productivity, DevOps, CI/CD, Empirical SE, Mining Software Repositories, Program Analysis, SE Research Methods.
- Research method: problem/assumption→claim→baseline→metrics→experiment→reproducibility→threats to validity.
- From Stage 2, include 1~3 RQ candidates/day with value, related existing problem, prerequisites, possible baseline/measurement; never assert novelty before current literature review.
