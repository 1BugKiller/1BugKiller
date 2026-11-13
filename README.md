### Backend engineer working on RAG systems

I build and fix the plumbing that makes retrieval-augmented generation work in
production: document ingestion, doc-store engine connectors, and the HTTP layer
that streams answers to clients.

**Currently**

- Contributing upstream to [RAGFlow](https://github.com/infiniflow/ragflow) —
  the Go backend: ingestion pipeline, Elasticsearch / OpenSearch / Infinity
  connectors, SSE streaming.
- MSc research on whether a generated answer is actually supported by the
  retrieved evidence (*groundedness*), and how minimal factual perturbations in
  that evidence break existing detectors.

**Upstream contributions**

| Change | What was wrong | Status |
|---|---|---|
| [ragflow#21439](https://github.com/infiniflow/ragflow/pull/21439) | Go ingestion: a chunk whose cleaned text was empty still entered the embedding batch, so the provider rejected the whole batch | merged |
| [ragflow#21656](https://github.com/infiniflow/ragflow/pull/21656) | Go HTTP: agent chat and bot completion streams were cut at the server's fixed 180 s write timeout because the deadline was never cleared | merged |
| [ragflow#21567](https://github.com/infiniflow/ragflow/pull/21567) | OpenSearch connector: deep pagination over more than 10k documents failed with `from + size = 11000` | open |
| [LightRAG#4262](https://github.com/HKUDS/LightRAG/pull/4262) | Parser: reject dot-prefixed paths inside a ZIP bundle | open |

Each change ships with a regression test that fails on the previous revision.
Where a fix could be undone by a later refactor, I add a source-level guard
test instead of a comment.

**How I work**

- Reproduce first, then read the code path — a fix without a failing test is a guess.
- Probe the claim before believing it; measure it, do not infer it.
- Keep the diff to the reported problem. Unrelated findings get their own issue.

<sub>中文：RAG 系统工程与 Go 后端，向上游 RAGFlow 提交修复（文档摄入、文档引擎连接器、SSE 流式）；研究 RAG 生成的答案是否真正被检索到的证据支持。</sub>
