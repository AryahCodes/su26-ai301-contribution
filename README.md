# AI301 Open Source Contribution

## Contributor

**Name:** Aryahvishwa Babu
**GitHub:** [AryahCodes](https://github.com/AryahCodes)
**Course:** CodePath AI301 Open Source Capstone Summer 2026

---

# Contribution 1: Moss OpenAI Agents SDK Cookbook

## Project

**Repository:** [usemoss/moss](https://github.com/usemoss/moss)
**Issue:** [#92 - Feature: OpenAI Agents SDK Cookbook](https://github.com/usemoss/moss/issues/92)
**My Fork:** [AryahCodes/moss](https://github.com/AryahCodes/moss)
**Working Branch:** [fix-issue-92-openai-agents-cookbook](https://github.com/AryahCodes/moss/tree/fix-issue-92-openai-agents-cookbook)

---

## Phase I: Issue Selection

### Selected Issue

I selected issue #92 from the Moss repository. The issue asks for a cookbook example showing how to connect Moss semantic search with the OpenAI Agents SDK.

The requested example should show how to:

1. Load a Moss index locally using `load_index()`.
2. Wrap `client.query()` as an OpenAI Agents SDK tool using the `@function_tool` decorator.
3. Support tool arguments for `query`, `top_k`, and optional metadata `filter`.
4. Run an end-to-end agent example where the agent receives a question, calls the Moss retrieval tool, and returns a grounded answer.
5. Include a README explaining metadata filters and the local-vs-cloud speed tradeoff.

### Why I Chose This Issue

I chose this issue because it connects directly to AI agents, retrieval tools, and semantic search. The scope is also realistic for an open-source first contribution because it is a cookbook/example contribution rather than a large core-library change.

This issue is also useful for future Moss users because examples make it easier for new developers to understand how to use the project in real applications.

### Current Issue Status

Issue #92 is still open. There is an existing linked PR, #146, that attempts to add the OpenAI Agents SDK cookbook example, but it has not been merged yet.

Because of that, I am treating the issue as still active while being careful not to duplicate work that already exists. My current plan is to review the existing PR, compare it against the issue requirements, and identify whether there are remaining bugs, documentation gaps, or test issues that I can help fix.

---

# Phase II: Reproduce & Plan

## Reproduction Process

### Environment Setup

I set up the Moss repository locally by working from my fork and adding the original Moss repository as the upstream remote.

Commands used:

```bash
git remote add upstream https://github.com/usemoss/moss.git
git fetch upstream
git checkout main
git pull origin main
git checkout -b fix-issue-92-openai-agents-cookbook
git push origin fix-issue-92-openai-agents-cookbook
```

This created and pushed my working branch for Phase II:

```text
https://github.com/AryahCodes/moss/tree/fix-issue-92-openai-agents-cookbook
```

I also confirmed that I was on the correct branch locally:

```bash
git branch
```

Output:

```text
* fix-issue-92-openai-agents-cookbook
  main
```

### Steps to Reproduce

1. Open the Moss repository locally.

2. Confirm that I am on my working branch:

```bash
git branch
```

3. Check the existing cookbook examples:

```bash
ls examples/cookbook
```

4. The output was:

```text
agentphone
autogen
crewai
daytona
dspy
generalist-moss-voice-agent
haystack
langchain
langgraph
mastra
moss-cognee-daytona
pydantic-ai
sim
```

5. Expected behavior:

There should be an `examples/cookbook/openai-agents/` directory because issue #92 requests a cookbook example for using Moss with the OpenAI Agents SDK.

6. Actual behavior:

There is no `openai-agents` directory under `examples/cookbook/` on the current branch.

This reproduces the missing cookbook issue locally. The project has multiple existing cookbook examples for other agent frameworks and retrieval integrations, but the OpenAI Agents SDK cookbook requested in issue #92 is not present on the current branch.

### Reproduction Evidence

Working branch:

```text
https://github.com/AryahCodes/moss/tree/fix-issue-92-openai-agents-cookbook
```

Local command used to reproduce the missing cookbook:

```bash
ls examples/cookbook
```

The command showed cookbook folders for other frameworks such as LangChain, LangGraph, CrewAI, AutoGen, DSPy, Haystack, Pydantic AI, and others, but no `openai-agents` folder.

---

## Solution Approach

### Implementation Plan

**Understand:**
Issue #92 asks for a cookbook example that shows how to connect Moss semantic search with the OpenAI Agents SDK. The example should load a Moss index locally using `load_index()`, wrap `client.query()` as an OpenAI Agents SDK `@function_tool`, support `query`, `top_k`, and optional metadata filters, and include an end-to-end agent run that returns a grounded answer.

The core problem is not a runtime bug in the current main branch. Instead, the problem is that the requested cookbook example is missing from the repository.

**Match:**
The Moss repository already has cookbook examples under `examples/cookbook/` for frameworks and tools such as LangChain, LangGraph, CrewAI, AutoGen, DSPy, Haystack, Pydantic AI, and others. I will use these examples as references for the expected folder structure, README style, setup instructions, and demo format.

I will also review PR #146 because it already attempts to solve this issue. My goal is to avoid duplicating that work and instead find a focused contribution opportunity if the existing PR has bugs, missing documentation, or incomplete acceptance criteria.

**Plan:**

1. Review the existing cookbook examples under `examples/cookbook/`.
2. Compare their structure and README style so the OpenAI Agents SDK cookbook follows the same pattern.
3. Review issue #92’s acceptance criteria carefully.
4. Review PR #146 because it already attempts to add the OpenAI Agents SDK cookbook.
5. Test whether the example from PR #146 runs locally.
6. Check whether the PR correctly handles:

   * `load_index()` before the agent runs
   * `@function_tool` usage from the OpenAI Agents SDK
   * `query`, `top_k`, and optional `filter` tool arguments
   * metadata filter examples
   * local-vs-cloud speed explanation in the README
   * an end-to-end agent run that returns a grounded answer
7. If PR #146 has confirmed bugs or missing documentation, I will make a focused contribution that fixes one of those gaps.
8. If PR #146 gets merged and fully solves issue #92 before I contribute, I will pivot to another Moss issue instead of opening a duplicate PR.

**Files I expect to inspect or modify:**

```text
examples/cookbook/openai-agents/README.md
examples/cookbook/openai-agents/moss_openai_agents.py
examples/cookbook/openai-agents/example_usage.py
examples/cookbook/openai-agents/test_live.py
```

The exact file names may change depending on what already exists in PR #146 and what structure best matches the rest of the Moss cookbook examples.

**Review:**
Before opening a PR, I will review the Moss repository’s contribution guidelines and make sure my changes are small, focused, and tied directly to issue #92 or to review feedback on PR #146. I will avoid making unrelated cleanup changes.

**Evaluate:**
I will verify the work by:

1. Running the cookbook example locally.
2. Confirming that the agent can call the Moss retrieval tool.
3. Confirming that `query` and `top_k` work as tool arguments.
4. Testing at least one metadata filter example.
5. Checking that `load_index()` is actually called before querying.
6. Reading the README instructions from the perspective of a new user and making sure the setup/run steps are clear.
7. Running any relevant tests or example commands included with the cookbook.

---

## Current Status

Phase II is complete because I have:

1. Set up the Moss repository locally.
2. Created and pushed my working branch.
3. Reproduced the missing cookbook issue by confirming that `examples/cookbook/openai-agents/` is not present.
4. Documented clear reproduction steps.
5. Written an implementation plan for how I will review, test, and potentially contribute to issue #92.

Next, I will move into Phase III by reviewing PR #146 in more detail and identifying a focused implementation, testing, or documentation contribution.
