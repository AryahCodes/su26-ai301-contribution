# Contribution 1: [Feature]: OpenAI Agents SDK Cookbook

**Contribution Number:** 1
**Student:** Aryahvishwa Babu
**Issue:** https://github.com/usemoss/moss/issues/92
**Status:** Phase I — Complete / Monitoring Existing PR

---

## Why I Chose This Issue

I chose this issue because it connects directly to my interest in AI agents, retrieval systems, and practical machine learning tools. The issue asks for a cookbook example showing how Moss can be used with the OpenAI Agents SDK as a retrieval tool. This stood out to me because I have worked with semantic search and AI-related projects before, so this issue gives me a chance to contribute to an open-source project that is closely related to my technical interests.

I also chose this issue because it has a clear scope and is labeled as a good first issue. Instead of changing a large internal part of the codebase, the contribution focuses on building a developer-facing example that helps users understand how to connect Moss retrieval with an agent workflow. I hope to learn more about how production-style AI agents use retrieval tools, how cookbook examples are structured in open-source projects, and how to write documentation that is useful for developers.

One important thing I noticed during issue selection is that another contributor has already submitted PR #146 for this issue. Because of that, I may need to either help review/test the existing PR, look for requested changes from the maintainers, or switch to another issue if this one gets merged before I can contribute meaningfully.

---

## Understanding the Issue

### Problem Description

The project is missing a cookbook example that shows how to use Moss together with the OpenAI Agents SDK. Moss provides semantic search functionality, but a new user may not immediately understand how to expose Moss search as a tool that an AI agent can call during an end-to-end run.

In my own words, the missing feature is an example that connects three pieces together: loading a Moss index locally, wrapping Moss search as an agent tool, and having an agent call that tool to answer a user question with retrieved context.

### Expected Behavior

The expected behavior is that the repository should include an example under:

`examples/cookbook/openai-agents/`

The example should show how to:

1. Load a Moss index locally using `load_index()` before querying.
2. Wrap `client.query()` as a function tool using the OpenAI Agents SDK `@function_tool` decorator.
3. Accept `query`, `top_k`, and an optional metadata `filter` as tool arguments.
4. Run an end-to-end agent example where the agent receives a question, calls the Moss retrieval tool, and returns a grounded answer.
5. Include a short README explaining when to use metadata filters and the local-vs-cloud speed tradeoff.

### Current Behavior

Currently, issue #92 is still open, but there is already an open pull request, PR #146, that appears to address the issue. The issue page shows that another contributor submitted a PR and said it follows the cookbook pattern, includes tool wrappers using `@function_tool`, and supports metadata filters.

Because of this, the issue may no longer be fully available for a new implementation from scratch. My next step is to review the linked PR and see whether there are still ways to contribute, such as testing the example, improving documentation, fixing maintainer feedback, or helping with missing acceptance criteria.

### Affected Components

The main parts of the codebase involved are:

* `examples/` — this is where project examples are stored.
* `examples/cookbook/openai-agents/` — this is the expected location for the new cookbook example.
* `README.md` inside the new example folder — this should explain setup, usage, metadata filters, and the local-vs-cloud speed tradeoff.
* Moss Python SDK usage — the example should use Moss index loading and querying.
* OpenAI Agents SDK usage — the example should use `@function_tool` and an end-to-end agent run.

---

## Reproduction Process

### Environment Setup

For Phase I, I reviewed the issue page, acceptance criteria, labels, comments, and linked pull request information. I also created/forked the relevant repositories needed to track my contribution work.

I have not started local implementation yet because I first need to check whether PR #146 already completes the issue. Since the issue has an existing open PR, the correct next step is to inspect that PR before duplicating work.

### Steps to Reproduce

Since this is a missing-feature issue, the reproduction process is not about triggering a runtime bug. Instead, reproduction means confirming whether the requested cookbook example exists and whether the issue is still available.

1. Open the Moss repository.
2. Navigate to issue #92.
3. Read the issue description and acceptance criteria.
4. Check the comments and linked development activity.
5. Notice that PR #146 has already been submitted for this issue.
6. Determine whether the issue is still a good candidate or whether I should contribute by testing/reviewing the existing PR.

### Reproduction Evidence

* **Issue link:** https://github.com/usemoss/moss/issues/92
* **Linked PR:** https://github.com/usemoss/moss/pull/146
* **My findings:** I found that issue #92 is still open and labeled as a good first issue, but another contributor has already submitted PR #146. This means I should not blindly implement the same solution from scratch. I need to review the existing PR and see whether there is still useful work to do.

---

## Solution Approach

### Analysis

The original root cause is that Moss needs a cookbook example showing how to connect Moss retrieval to an OpenAI Agents SDK agent. The desired example should demonstrate local index loading, a function tool wrapper around `client.query()`, metadata filter support, and an end-to-end agent run.

However, after reviewing the issue activity, the main contribution risk is that another PR may already solve the issue. If PR #146 satisfies all acceptance criteria and gets merged, this issue will no longer be a good choice for my own contribution. If PR #146 is incomplete or receives maintainer feedback, I may still be able to contribute by testing, improving documentation, or helping address gaps.

### Proposed Solution

My proposed next step is to inspect PR #146 and compare it against the acceptance criteria from issue #92.

I will check whether the PR:

1. Adds the example under `examples/cookbook/openai-agents/`.
2. Calls `load_index()` before the agent runs.
3. Uses the OpenAI Agents SDK `@function_tool` decorator.
4. Supports `query`, `top_k`, and optional `filter` arguments.
5. Includes a README explaining metadata filters and the local-vs-cloud speed tradeoff.

If the PR is incomplete, I can contribute by suggesting or implementing missing pieces. If the PR is complete, I should switch to another open issue before spending too much time on this one.

### Implementation Plan

Using the UMPIRE framework:

**Understand:**
The issue asks for a cookbook example that demonstrates Moss being used as a retrieval tool inside an OpenAI Agents SDK agent. The example should load a Moss index first, define a tool around `client.query()`, support `query`, `top_k`, and optional `filter`, and then show an agent answering a question using retrieved results.

**Match:**
I will compare the requested cookbook example with existing examples in the Moss repository and with PR #146. I will look for similar cookbook patterns, especially how example folders, README files, and tool integrations are structured.

**Plan:**

1. Review issue #92 and write down the acceptance criteria.
2. Open PR #146 and inspect the changed files.
3. Compare PR #146 against the acceptance criteria.
4. If the PR is missing something, identify a small improvement I can make.
5. If the PR is complete, choose a different issue before Phase II.
6. If contributing to this issue is still possible, fork the repository and create a branch.
7. Make a focused change, such as documentation improvement, testing improvement, or missing acceptance criteria fix.
8. Run the example or relevant tests.
9. Document the results in this README.
10. Submit a PR only if there is a real gap to fix.

**Implement:**
Branch/commit links:

* Branch: Not started yet
* Commit 1: Not started yet
* Commit 2: Not started yet

**Review:**

Self-review checklist:

* [ ] I checked whether PR #146 already solves the issue.
* [ ] I avoided duplicating another contributor’s work.
* [ ] I compared the existing PR against the issue acceptance criteria.
* [ ] I identified whether there is still useful work I can do.
* [ ] If I continue with this issue, my change is focused and non-duplicative.
* [ ] If I switch issues, I document why.

**Evaluate:**
I will evaluate whether this is still a valid contribution by reviewing PR #146. If there is no meaningful remaining work, I will switch issues rather than waste time or submit a duplicate PR.

---

## Testing Strategy

### Unit Tests

Since this issue is mostly about a cookbook/documentation example, traditional unit tests may not be required. However, if I contribute to the example, I should still verify the important behavior.

* [ ] Test case 1: Confirm that `load_index()` is called before the agent runs.
* [ ] Test case 2: Confirm that the retrieval tool accepts a normal query.
* [ ] Test case 3: Confirm that the optional metadata filter argument is handled.

### Integration Tests

* [ ] Integration scenario 1: Run the full cookbook example.
* [ ] Integration scenario 2: Confirm the agent can call the Moss retrieval tool.
* [ ] Integration scenario 3: Confirm the final answer uses retrieved context.

### Manual Testing

Not completed yet. My next step is to inspect PR #146 and determine whether there is still a contribution opportunity.

---

## Implementation Notes

### Week 1 Progress

This week, I selected issue #92 from the Moss repository and started Phase I of the contribution process. I reviewed the issue description, acceptance criteria, labels, and comments. I also noticed that another contributor had already submitted PR #146 for this issue.

This changed my plan. Instead of immediately starting a duplicate implementation, I need to review the existing PR and determine whether it fully satisfies the issue. If the PR is incomplete, I may contribute by testing it or improving missing parts. If it already completes the issue, I will switch to another issue before Phase II.

### Week 2 Progress

Not started yet.

### Code Changes

* **Files modified:** None yet.
* **Key commits:** None yet.
* **Approach decisions:** I decided not to start coding immediately because the issue already has an open PR. This is important because submitting duplicate work would not be useful to the project. My next step is to inspect the existing PR and look for a meaningful way to contribute.

---

## Pull Request

**PR Link:** Not submitted yet.

**PR Description:**
Not applicable yet.

**Maintainer Feedback:**

* No maintainer feedback yet.

**Status:** Monitoring existing PR / deciding whether to continue or switch issues.

---

## Learnings & Reflections

### Technical Skills Gained

Through this issue selection process, I learned that choosing an open-source issue is not only about whether the issue is interesting. It is also important to check whether someone else is already working on it, whether there is an open PR, and whether there is still meaningful work left to do.

### Challenges Overcome

The main challenge was realizing that even though the issue is open and labeled as a good first issue, there is already a linked PR that may solve it. I handled this by adjusting my plan instead of blindly continuing.

### What I’d Do Differently Next Time

Next time, I would check the linked pull requests and recent comments before commenting that I want to work on an issue. That would help me avoid choosing an issue that may already be close to completion.

---

## Resources Used

* GitHub issue #92: https://github.com/usemoss/moss/issues/92
* Linked PR #146: https://github.com/usemoss/moss/pull/146
* Moss repository: https://github.com/usemoss/moss
* Moss documentation: https://docs.moss.dev
* OpenAI Agents SDK documentation: https://openai.github.io/openai-agents-python/
