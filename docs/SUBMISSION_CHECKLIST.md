# Amazon Developer Hackathon 2026 — Submission Checklist

**Target submission:** 22 October 2026, leaving 23 October as a buffer. The official deadline shown by Devpost is 23 October 2026 at 12:00 p.m. Pacific Time. Re-check the live submission form before final submission.

**Official sources (accessed 2026-10-14):**
- Rules: https://amazonappdev2026.devpost.com/rules
- Hackathon FAQ: https://amazonappdev2026.devpost.com/details/faqs
- Main event page: https://amazonappdev2026.devpost.com/

Do not check an item until the repository, actual implementation, or submission form provides evidence. This checklist records official requirements and outstanding proof; it does not assert the current code already satisfies them.

## 1. Primary track: Alexa+

- [ ] Select Alexa+ as the primary track in the submission form.
- [ ] Implement a functioning self-hosted MCP server using MCP specification 2025-11-25 or later over Streamable HTTP.
- [ ] Pin and document the compatible MCP SDK version.
- [ ] Ensure MCP is used at runtime: actual server entry point, protocol initialization/transport, registered tools, and tool calls—not just a README mention.
- [ ] Build a web voice client that acts as a genuine MCP client and invokes the server through MCP protocol traffic.
- [ ] Demonstrate the client and server functioning together in the video.
- [ ] State accurately that this is Veto's web voice client and not a live connection into the Alexa+ assistant. The official FAQ says the gated Alexa+ preview tools are unavailable to hackathon participants and recommends a self-hosted MCP server or a web-based simulator/front end.

## 2. Mini-challenge: AWS Builder

- [ ] Select AWS Builder as a mini-challenge.
- [ ] Implement and verify the AWS integrations actually used; do not list planned services as completed integrations.
- [ ] Document each AWS service and its role in Product Feedback, with setup/onboarding experience, what worked, what needs work, and whether we'd build with it again.
- [ ] For the selected architecture, verify and document:
  - [ ] Lambda hosting for MCP HTTP endpoint.
  - [ ] FastAPI scoring endpoint deployed to Lambda through Mangum.
  - [ ] DynamoDB single-table persistence and user-scoped access patterns.
  - [ ] Bedrock Nova Lite default narration; Claude Haiku only if actually supported/configured/used.
  - [ ] Polly voice output if actually integrated and demonstrated.
- [ ] Include deployment/service/configuration evidence and cost/region caveats where relevant.
- [ ] Ensure local mode also runs without AWS credentials; clearly distinguish local adapters/fallbacks from AWS services.
- [ ] Verify least-privilege IAM, no secrets in source, safe logging, and a teardown plan.
- [ ] Do not claim the AWS Builder mini-challenge until the submission demonstrates documented AWS service integrations.

## 3. Mini-challenge: Open Source

- [ ] Select Open Source as a mini-challenge.
- [ ] Keep the Veto repository public: https://github.com/Cyberangelo-King/Veto
- [ ] Ensure a plain standard MIT License is present at repository root and GitHub detects/displays the license near the top of the public repository page.
- [ ] Confirm LICENSE reads “Copyright (c) 2026 Faith Akinola Boyejo”.
- [ ] Do not imply MIT covers datasets, model artifacts, dependencies, fonts, icons, images, brands, or external services.
- [ ] Record the exact contribution URL (for example, the relevant PR or branch), repository URL, GitHub username Cyberangelo-King, and a short description of what changed, how it works, and why it matters.
- [ ] Ensure the contribution/repository work was created during the hackathon window and is additional to the primary-track demonstration.
- [ ] The official rules permit a branch/PR contribution to remain unmerged; do not claim a PR is merged unless it is.

## 4. Repository setup and run instructions

- [ ] README describes the selected product, limitations, architecture, and actual implemented features.
- [ ] Add tested prerequisites and exact commands for local setup, dependencies, environment configuration, data preparation, running each service, launching the web client, and running tests.
- [ ] Explain how to obtain the dataset without committing raw CSV files; document source, access date, visible terms/license, and attribution requirements.
- [ ] Provide a placeholder-only environment template; secrets must remain local or in an approved secret manager.
- [ ] Provide deterministic seed/demo fixtures and exact reset instructions.
- [ ] Document local mode with no AWS credentials, plus separately verified AWS mode.
- [ ] Document error handling, common setup failures, and how to shut down/tear down resources.
- [ ] Provide a clear statement that financial actions are simulated and the model is not a production fraud-prevention service.
- [ ] Verify these instructions on a clean environment or fresh checkout; don't mark complete based only on the author's machine.

## 5. Public demonstration video

- [ ] Upload the video publicly to YouTube or Vimeo and include its URL in Devpost.
- [ ] Keep the official video under three minutes; Veto's internal hard cap is 2:50.
- [ ] Show the project actually functioning on the intended platform; include the web voice client, the MCP tool call path, scoring/explanation, prompt-injection handling, and cancel-then-confirm simulated freeze.
- [ ] Use English narration/text or provide the required English translation for non-English materials.
- [ ] Avoid third-party trademarks and copyrighted music/footage unless permission is held.
- [ ] Do not hide failures through editing or imply that simulated actions affect a real bank/card.
- [ ] Ensure the recording matches the submission commit and contains no credentials or private data.

## 6. Required product feedback — one section per tool, API, or SDK used

For each tool, API, SDK, and relevant developer service actually used, answer:
- [ ] Which tool/API/SDK was used, and for what?
- [ ] What worked well (setup, documentation, testing, performance, reliability)?
- [ ] What needs work (errors, missing documentation/features, compatibility issues, limitations, workarounds)?
- [ ] What was the onboarding experience from zero to first working result?
- [ ] Would we build with it again? Yes/No, with a reason.
- [ ] Include the version and an evidence-backed example where possible.

Create separate feedback for the MCP SDK/protocol implementation, web voice/browser APIs, Python/FastAPI/Mangum path, and each AWS service actually used. For AWS Builder, explicitly name the AWS services and describe exactly how each was integrated. Do not submit generic praise or invented friction.

## 7. Track and mini-challenge declarations

- [ ] Identify Alexa+ as the primary track.
- [ ] Identify AWS Builder and Open Source as mini-challenges.
- [ ] Complete every required field in the submission form.
- [ ] If asked how the project changed during the hackathon period, list actual commits/PRs and demonstrate those changes.

## 8. Optional feature requests

- [ ] Submit only useful, specific feature requests.
- [ ] For each request, explain what should be built, why it matters, and assign the official priority: Critical / Important / Nice-to-have.
- [ ] Distinguish an actual missing capability encountered from a speculative idea.

## 9. Optional friction log — up to 10% judging bonus

- [ ] Include observed tool friction only; do not fabricate incidents for bonus points.
- [ ] Each entry contains: task attempted, tool, steps taken, expected result, actual result, severity (Critical/High/Medium/Low), workaround used, actionable suggestion, date, and sanitized evidence.
- [ ] Ensure the entry is specific enough for a tool team to reproduce and act on.
- [ ] Link the entries from the submission form if requested. The official rules state that friction logs can provide up to a 10% judging bonus.

## 10. Final honesty, licensing, and access checks

- [ ] All features shown in video work in the submitted version.
- [ ] No unverified performance or accuracy metrics.
- [ ] Dataset/model provenance, licenses, and attribution are documented.
- [ ] No real card numbers, CVVs, PINs, banking credentials, or customer transaction records.
- [ ] No unsupported claims of real fraud prevention, regulatory compliance, or live bank actions.
- [ ] Judges can access the repository/demo/video free of charge and without unintended restrictions through the judging period.
- [ ] The final URL, repository, contribution URL, and GitHub username in Devpost are correct.
- [ ] Re-open the official rules and FAQ before submitting in case requirements changed.
