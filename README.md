# Contribution 1: [Feature]: OpenAI Agents SDK Cookbook

**Contribution Number:** 1
**Student:** Aryahvishwa Babu
**Issue:** https://github.com/usemoss/moss/issues/92
**Status:** Phase I — In Progress

---

## Why I Chose This Issue

I chose this issue because it connects directly to my interest in AI agents, retrieval systems, and practical machine learning tools. The issue asks for a cookbook example showing how Moss can be used with the OpenAI Agents SDK as a retrieval tool. This stood out to me because I have worked with semantic search and AI-related projects before, so this issue gives me a chance to contribute to an open-source project that is closely related to my technical interests.

I also chose this issue because it is a good first issue with a clear scope. Instead of changing a large internal part of the codebase, the contribution focuses on building an example that helps future users understand how to connect Moss retrieval with an agent workflow. I hope to learn more about how production-style AI agents use retrieval tools, how cookbook examples are structured in open-source projects, and how to write documentation that is useful for developers.

---

## Understanding the Issue

### Problem Description

The project is missing a cookbook example that shows how to use Moss together with the OpenAI Agents SDK. Moss already provides semantic search and local index loading, but a new user may not immediately understand how to expose Moss search as a tool that an AI agent can call during an end-to-end run.

In my own words, the missing part is an example that connects three pieces together: loading a Moss index locally, wrapping Moss search as an agent tool, and having an agent call that tool to answer a user question with retrieved context.

### Expected Behavior

The expected behavior is that the repository should include an example under:

`examples/cookbook/openai-agents/`

The example should show how to:

1. Load a Moss index before the agent runs.
2. Wrap `client.query()` as a function tool using the OpenAI Agents SDK `@function_tool` decorator.
3. Accept `query`, `top_k`, and an optional metadata `filter` as tool arguments.
4. Run an end-to-end agent example where the agent receives a question, calls the Moss retrieval tool, and returns a grounded answer.
5. Include a short README explaining when to use metadata filters and the local-vs-cloud speed tradeoff.

### Current Behavior

Currently, the issue indicates that this specific OpenAI Agents SDK cookbook example does not exist. Because of that, users who want to use Moss with an OpenAI agent have to figure out the integration themselves by reading separate Moss documentation and OpenAI Agents SDK documentation.

### Affected Components

The main parts of the codebase involved are:

* `examples/` — this is where the new cookbook example should be added.
* `examples/cookbook/openai-agents/` — this is the expected location for the new example.
* `README.md` inside the new example folder — this should explain how to run the example and when to use metadata filters.
* Moss Python SDK usage — the example will likely use `MossClient`, `load_index()`, and `client.query()`.
* OpenAI Agents SDK usage — the example will use `@function_tool` and an agent run.

---

## Reproduction Process

### Environment Setup

For Phase I, I started by reviewing the GitHub issue and the Moss repository structure. I looked at the issue requirements and checked where examples are stored in the repository. The main setup work is to fork the repository, clone it locally, install the project dependencies, and create a new branch for the cookbook contribution.

**ONLY_FILL_THIS:** Add your exact setup commands here after you do them. For example:

```bash
git clone https://github.com/YOUR_USERNAME/moss.git
cd moss
git remote add upstream https://github.com/usemoss/moss.git
git checkout -b openai-agents-cookbook
```

One setup challenge I expect is making sure the Moss SDK and OpenAI Agents SDK dependencies are installed correctly in the same Python environment. Another likely challenge is safely handling API keys through environment variables instead of hardcoding credentials.

### Steps to Reproduce

Since this is a missing-feature issue, the reproduction process is not about triggering a bug. Instead, the reproduction is confirming that the requested cookbook example does not currently exist.

1. Open the Moss GitHub repository.
2. Navigate to the `examples/` directory.
3. Search for an OpenAI Agents SDK cookbook example.
4. Confirm that there is no complete example showing Moss as a retrieval tool for an OpenAI agent.
5. Compare the current repository examples against the acceptance criteria from issue #92.

### Reproduction Evidence

* **Commit showing reproduction:** ONLY_FILL_THIS
* **Screenshots/logs:** ONLY_FILL_THIS
* **My findings:** I found that the requested example is not currently present in the expected cookbook location. The issue is not a runtime bug, but a missing developer-facing example. The contribution should add a clear, runnable example and README.

---

## Solution Approach

### Analysis

The root cause is that Moss has retrieval functionality, but there is no dedicated cookbook example showing how to expose that retrieval functionality to the OpenAI Agents SDK. A user could call Moss directly, but the missing documentation/example makes it harder to understand how Moss fits into an agentic workflow.

The issue specifically asks for an example that demonstrates local index loading before querying. This is important because Moss emphasizes fast retrieval after loading an index locally. The example should not silently skip `load_index()` because that would miss one of the main points of the cookbook.

### Proposed Solution

My proposed solution is to add a new cookbook folder:

`examples/cookbook/openai-agents/`

Inside that folder, I would add:

1. A Python example file showing the full agent workflow.
2. A README explaining setup, environment variables, how to run the example, metadata filtering, and the local-vs-cloud speed tradeoff.
3. Optional sample data or comments showing how the user should create or load an index before querying.

The example should be simple enough for a new user to understand, but complete enough to satisfy the issue acceptance criteria.

### Implementation Plan

Using the UMPIRE framework:

**Understand:**
The issue asks for a cookbook example that demonstrates Moss being used as a retrieval tool inside an OpenAI Agents SDK agent. The example should load a Moss index first, define a tool around `client.query()`, support `query`, `top_k`, and optional `filter`, and then show an agent answering a question using retrieved results.

**Match:**
I will look at existing examples in the Moss repository to match the project’s style. I will also look at OpenAI Agents SDK examples to follow the expected pattern for `@function_tool`, agent creation, and running the agent.

**Plan:**

1. Create a new folder: `examples/cookbook/openai-agents/`.
2. Add a Python example file, likely named `main.py` or `openai_agents_moss.py`.
3. Initialize a Moss client using environment variables for credentials.
4. Call `load_index()` before the agent is created or before the agent runs.
5. Define a function tool using the OpenAI Agents SDK `@function_tool` decorator.
6. The tool should accept:

   * `query`
   * `top_k`
   * optional `filter`
7. Inside the tool, call `client.query()` and return the retrieved documents in a readable format.
8. Create an agent that has access to the Moss retrieval tool.
9. Run the agent with a sample user question.
10. Add a README explaining setup, usage, metadata filters, and local-vs-cloud retrieval tradeoffs.
11. Manually test the example.
12. Submit a pull request and respond to maintainer feedback.

**Implement:**
Branch/commit links:

* Branch: ONLY_FILL_THIS
* Commit 1: ONLY_FILL_THIS
* Commit 2: ONLY_FILL_THIS

**Review:**

Self-review checklist:

* [ ] The example is placed under `examples/cookbook/openai-agents/`.
* [ ] The example calls `load_index()` before querying.
* [ ] The tool uses the OpenAI Agents SDK `@function_tool` decorator.
* [ ] The tool schema includes `query`, `top_k`, and optional `filter`.
* [ ] The agent performs an end-to-end run.
* [ ] The README explains metadata filters.
* [ ] The README explains local-vs-cloud speed tradeoffs.
* [ ] API keys are not hardcoded.
* [ ] The code style matches the repository’s examples.
* [ ] Manual testing confirms the example runs or the setup limitations are clearly documented.

**Evaluate:**
I will verify the solution by running the cookbook example locally. I will check that the Moss index is loaded before querying, the agent can call the retrieval tool, and the final response uses retrieved context. I will also review the README to make sure a new user can understand how to run the example without needing to inspect the code deeply.

---

## Testing Strategy

### Unit Tests

Since this is primarily a cookbook/documentation example, full unit tests may not be necessary unless the maintainers request them. However, I can still check the important behavior manually or through a lightweight test.

* [ ] Test case 1: Confirm that `load_index()` is called before the agent runs.
* [ ] Test case 2: Confirm that the retrieval tool accepts a normal query and returns results.
* [ ] Test case 3: Confirm that the optional metadata filter can be passed without breaking the tool.

### Integration Tests

* [ ] Integration scenario 1: Run the full example and confirm the agent calls the Moss retrieval tool.
* [ ] Integration scenario 2: Run the example with a metadata filter and confirm the tool still works.
* [ ] Integration scenario 3: Run the example with a different `top_k` value and confirm the number of retrieved results changes appropriately.

### Manual Testing

**ONLY_FILL_THIS:** After running the example, write what happened here.

Example wording:

I manually tested the cookbook by running:

```bash
python examples/cookbook/openai-agents/main.py
```

The example successfully loaded the Moss index, created the retrieval tool, ran the agent, and returned an answer based on retrieved documents. I also tested changing `top_k` and passing a metadata filter to confirm the tool arguments worked as expected.

---

## Implementation Notes

### Week 1 Progress

**ONLY_FILL_THIS:** Write what you actually did in Week 1.

Suggested version if you only researched and set up:

This week, I selected issue #92 from the Moss repository and started Phase I of the contribution. I reviewed the issue requirements, read through the repository structure, and identified that the contribution should go under `examples/cookbook/openai-agents/`. I also began setting up my local development environment by forking and cloning the repository.

The main thing I learned this week is that this issue is not a traditional bug fix. It is a missing-feature/documentation contribution where the goal is to create a working cookbook example. Because of that, reproduction means confirming the requested example is missing and understanding the acceptance criteria clearly before writing code.

### Week 2 Progress

**ONLY_FILL_THIS:** Add after you start coding.

Suggested version:

This week, I started implementing the cookbook example. I created the new example folder and began writing the Python script that connects Moss retrieval with the OpenAI Agents SDK. I focused on making sure the example calls `load_index()` before running the agent and that the retrieval function tool supports `query`, `top_k`, and optional metadata filters.

### Code Changes

* **Files modified:**

  * `examples/cookbook/openai-agents/main.py` — adds the end-to-end Moss + OpenAI Agents SDK example.
  * `examples/cookbook/openai-agents/README.md` — explains setup, running the example, metadata filters, and local-vs-cloud speed tradeoffs.
  * ONLY_FILL_THIS — add any other files you modify.

* **Key commits:**

  * ONLY_FILL_THIS — initial cookbook example.
  * ONLY_FILL_THIS — README and documentation updates.
  * ONLY_FILL_THIS — cleanup after testing/feedback.

* **Approach decisions:**
  I chose to keep the example focused and beginner-friendly because the issue is labeled as a good first issue. Instead of building a complex app, I focused on showing the core integration clearly: load a Moss index, expose search as an agent tool, and run an agent that answers a question using retrieved context.

---

## Pull Request

**PR Link:** ONLY_FILL_THIS

**PR Description:**

This PR adds a cookbook example for using Moss with the OpenAI Agents SDK. The example demonstrates how to load a Moss index locally, wrap `client.query()` as an OpenAI Agents SDK function tool, pass `query`, `top_k`, and optional metadata filter arguments, and run an end-to-end agent that uses Moss retrieval to answer a question.

The PR also includes a README explaining how to run the example, when metadata filters are useful, and why local index loading can improve retrieval speed compared with relying only on cloud calls.

**Maintainer Feedback:**

* ONLY_FILL_THIS: [Summary of feedback received]
* ONLY_FILL_THIS: [How you addressed it]

**Status:** Awaiting implementation / Awaiting review

---

## Learnings & Reflections

### Technical Skills Gained

Through this contribution, I am learning how retrieval systems can be connected to AI agents as tools. I am also learning how cookbook examples are structured in open-source projects, how to write developer-facing documentation, and how to make an example useful without making it unnecessarily complicated.

### Challenges Overcome

One challenge is understanding both sides of the integration: Moss retrieval and the OpenAI Agents SDK tool system. To handle this, I broke the problem down into smaller parts: first understanding how Moss loads and queries an index, then understanding how the Agents SDK defines tools, and finally connecting the two in one example.

### What I’d Do Differently Next Time

Next time, I would first search the repository for similar examples before writing anything. That would help me match the project’s style earlier and avoid making the example look disconnected from the rest of the codebase. I would also document my reproduction and setup steps earlier so the final contribution write-up is easier to complete.

---

## Resources Used

* GitHub issue #92: https://github.com/usemoss/moss/issues/92
* Moss repository: https://github.com/usemoss/moss
* Moss documentation: https://docs.moss.dev
* OpenAI Agents SDK documentation: https://openai.github.io/openai-agents-python/
