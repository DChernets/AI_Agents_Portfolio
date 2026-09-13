# Industrial Document Intelligence

**Business product for an industrial gas-cleaning engineering company**

**Status:** tender-analysis module implemented; contract-review application in pre-production hardening for an internal pilot.

## Business context

Industrial engineering teams receive large tender and contract packages assembled from Word and Excel files. Engineers and legal reviewers need to find requirements, identify risks and missing inputs, prepare revisions, and preserve a traceable link to the source documents.

The work is split into two product modules built around real company documents and review workflows.

## Tender documentation analysis

The implemented tender-analysis module:

- ingests tender packages and extracts their structure;
- identifies technical requirements and source-data references;
- highlights missing, inconsistent, or clarification-worthy inputs;
- prepares a structured summary for engineering review;
- keeps technical and commercial decisions with the company specialist.

## Contract Review application

The second module is a native macOS application for reviewing customer contracts from the Supplier's position. It is approaching an internal pilot and currently supports the full operator workflow:

1. The employee adds a contract and its attachments in a native desktop interface.
2. The application extracts the document structure and masks sensitive data locally.
3. Only the redacted package is sent to the LLM workflow for clause-level analysis against the company's rules and approved examples.
4. The reviewer accepts, edits, or removes each proposed change.
5. The application generates a Word draft of the disagreement protocol and can save explicitly approved feedback for later knowledge-base updates.

The product also includes saved review state, technical diagnostics without contract text, a local editable knowledge base, macOS packaging, and a private update channel.

## Product and engineering decisions

### Local privacy boundary

Source documents, replacement maps, and full review artifacts remain on the user's Mac. The external model receives only a redacted package after a local leak scan. Credentials and update access are stored in macOS Keychain.

### Human review before output

The LLM proposes findings and revisions; the company reviewer makes the decision. Word output is generated only after the review is complete. Test runs and real approved cases remain separate.

### Evidence and repeatability

The system keeps clause references, rule context, approved examples, and regression cases separate. Quality checks are run against fixed reference cases before changes are promoted to a release.

### Product delivery

The application is packaged as a native macOS app for the internal team. Updates are distributed through a private signed release workflow while user settings, review history, and knowledge-base changes remain outside the application bundle.

## My role

I work with the company's documents and subject-matter experts, define the operator workflow, design the product and system architecture, implement the application and LLM pipeline, package releases, review quality failures, and prepare the product for internal use.

## Technology

Python, document parsing, structured LLM outputs, rules and precedent retrieval, local redaction, Word generation, pywebview, SQLite, macOS packaging, private GitHub releases, and automated quality checks.

## Public case-study boundary

Customer documents, legal positions, source code, model prompts, credentials, and internal benchmark artifacts are intentionally not published. This page describes the workflow and engineering decisions without exposing confidential business data.
