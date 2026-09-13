# AI SMM for Wholesale Suppliers

**Active product for catalogue and Telegram publishing workflows**

## Business context

Wholesale suppliers regularly turn informal product photos and short descriptions into catalogue entries and Telegram posts. The work combines product recognition, image preparation, copywriting, pricing data, scheduling, and publication across several channels.

## Product workflow

The supplier sends one or more product photos to the Telegram bot. The system then:

- recognizes the product and extracts its attributes;
- improves the photo for use in a product card;
- generates editable marketing content;
- stores the item in the supplier's catalogue;
- schedules or publishes the item to connected Telegram channels.

The publishing workflow supports team access, channel-specific descriptions, publication windows, rate limits, and catalogue management. A separate support bot answers from the product knowledge base and classifies incoming support requests.

## Engineering decisions

### Human-controlled publishing

Generated product data and content remain editable before publication. Scheduling and channel settings are explicit so automation does not post to the wrong audience or time slot.

### Separate operational concerns

Product creation, catalogue state, publishing queues, rate limits, and support requests are handled as separate parts of the system. This keeps failures in one workflow from blocking the others.

### Privacy boundary

Contact details that do not need model processing are added locally. External AI calls receive only the information required for recognition, image work, or content generation.

## My role

I designed the user workflow, implemented the Telegram interfaces and AI pipelines, built the catalogue and scheduling logic, integrated Google services, and deployed the application for active use and iteration.

## Technology

Python, python-telegram-bot, Google Gemini, PostgreSQL, Redis, Google Sheets and Drive APIs, APScheduler, and Linux/systemd deployment.

## Public case-study boundary

User data, credentials, pricing rules, production configuration, and source code are private. This page describes the product workflow and architecture at a case-study level.
