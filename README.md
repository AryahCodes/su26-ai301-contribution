## Phase IV: Submit & Iterate

### Pull Request

**PR Link:**
https://github.com/usemoss/moss/pull/311

**PR Description:**
This pull request completes the remaining acceptance criteria for the OpenAI Agents + Moss cookbook. I updated the Moss retrieval tool so it accepts a configurable query, `top_k`, and optional metadata filter. I also added structured retrieval results containing document IDs, text, relevance scores, and metadata.

In addition, I added required environment-variable validation, updated the documentation, and created nine mocked unit tests that run without real API credentials or network access.

**Relevant Issue:**
Issue #92 — OpenAI Agents SDK Cookbook

### Testing

The following checks passed locally:

* `python -m unittest test_example.py`
* `python -m py_compile example.py test_example.py`
* `black --check example.py test_example.py`
* `git diff --check`

Test result:

```text
Ran 9 tests in 0.012s

OK
```

The upstream repository’s available CI checks are also passing.

### Maintainer Feedback and Next Steps

* A maintainer asked whether I had signed the Contributor License Agreement.
* I completed the CLA signing process.
* The pull request is currently waiting for review from a maintainer with write access.
* If changes are requested, I will update the same branch, push a follow-up commit, and respond to the reviewer.

### Status

**Awaiting review**

## Learnings & Reflections

This contribution helped me learn how an OpenAI Agent can use Moss as a retrieval tool. I learned how to expose configurable tool arguments, pass metadata filters into retrieval options, return structured grounding information, and write mocked tests for code that normally depends on external APIs.

The most important lesson was that submitting a pull request does not mean the code must already be perfect. Automated tests and maintainer review are part of the open-source development process.
