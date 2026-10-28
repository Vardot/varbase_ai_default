---
name: varbase-ai-base
description: "Apply, repair and verify Varbase AI Base on a Varbase 11 site: the provider setup (Drupal CMS AI), the Varbase AI Base stack and the one-step Varbase AI Default 2.x, and the order everything is applied in. Install and apply commands, inputs, config, post-apply steps, browser checks, traps and versions, read from the recipe code. Use when adding, fixing or checking Varbase AI Base."
---

# Varbase AI Base

Read from `recipe.yml`, `composer.json`, README, CHANGELOG and `git log` at the latest tag, 28 October 2026. Re-check versions on drupal.org before relying on them. For the full Varbase AI apply order, see the Varbase AI recipes docs page.

## Recipes

| Recipe | Latest | Stability | Require |
|---|---|---|---|
| `varbase_ai_base` | 1.0.3 | stable | `drupal/varbase_ai_base:~1` |
| `varbase_ai_default` | 2.0.0-alpha1 | alpha | `drupal/varbase_ai_default:~2` |

Docs (the code wins where they differ):
- https://docs.varbase.vardot.com/developers/understanding-varbase/varbase-ai-recipes/varbase-ai-base
- https://docs.varbase.vardot.com/developers/understanding-varbase/varbase-ai-recipes/varbase-ai-default

## What it does

- `varbase_ai_base` applies `drupal_cms_ai` (providers amazee.ai, OpenAI, Anthropic; keys; the `drupal_cms_assistant`; Canvas AI; Klaro), then `varbase_ai_image_alt`, `varbase_ai_editor_assistant`, `varbase_ai_taxonomy_tagging`, `varbase_ai_context`, `varbase_ai_content_review_base`, `varbase_ai_safety`. Installs `ai`, `eca`, `ai_integration_eca`. Turns on the Canvas tools of `ai_agents.ai_agent.drupal_cms_assistant`.
- Composer 1.0.3: `drupal/core ~11.4.0`, `drupal_cms_ai ~2`, `eca ~3`, `ai_integration_eca ~1`, `gemini_provider ^1.1`, `elevenlabs ^1.2`, every public sibling at `~1` (image alt, editor assistant, tagging at `~2.0.0`), and `varbase_ai_default ~2`. So requiring Base brings every Varbase AI recipe into the codebase; only the seven above are applied.
- `varbase_ai_default` 2.x applies Base, then `varbase_ai_vdb_mariadb`, `varbase_ai_search_base`, `varbase_ai_chatbot_base`, `varbase_ai_answers_base`, `varbase_ai_content_operations_base`, `varbase_ai_mcp_server_base`, `varbase_ai_readable_base`, `varbase_ai_seo`, `varbase_ai_media_base`, `varbase_ai_figma_base`. Milvus is left out.
- Inputs: a hidden `_form_trigger` collects the sub-recipe inputs so Project Browser shows them in one form. Main ones: `drupal_cms_ai.provider` (amazeeai, the trial), `drupal_cms_ai.openai_api_key`, `drupal_cms_ai.anthropic_api_key`, `varbase_ai_taxonomy_tagging.content_type` (page).

## Apply

All commands in DDEV, from the project root; recipes are applied from the docroot path `../recipes/<name>`. Take a snapshot first: `ddev snapshot --name before-varbase-ai-base`. Add each recipe to `extra.drupal-recipe-unpack.ignore` in `composer.json` before requiring it (read the list first: `composer config --json` replaces it).

```bash
ddev composer require drupal/varbase_ai_base:~1
ddev drush cr
ddev drush recipe ../recipes/varbase_ai_base -y --input=drupal_cms_ai.provider=openai
# Everything in one step (Varbase 11, alpha):
ddev drush en ai_answers -y && ddev drush cr
ddev drush recipe ../recipes/varbase_ai_default -y
ddev drush cr
```

Never type a key on the command line in a shared shell; leave the key inputs empty and add the keys in Configuration > System > Keys.

Full apply order: AI Base; one vector database recipe; Search Base; Chatbot and Answers; then content review, content operations, MCP, readable, SEO, media, Figma in any order. MCP and Readable need no AI provider.

## After the apply

- Set the default models in Configuration > AI > AI settings: chat, chat with tools, chat with image vision, embeddings, text to image.
- On Drupal CMS 2, do not apply Base as one recipe: `drush en ai_ckeditor ai_integration_eca`, `cr`, then apply its seven recipes one by one.

## Verify

- `ddev drush cget ai.settings default_providers` lists a provider per operation.
- In a browser as an editor: the AI dashboard loads, the CKEditor AI button shows, Suggest tags shows on the page form, the Review tab shows on a content item.

Test as a real editor or visitor, not user 1: a superuser bypasses permissions.

## Traps

- Drupal CMS 2: "cannot redeclare class" when applied as one recipe (enable `ai_ckeditor` first, apply by parts).
- Taxonomy tagging 2.0.1 and older defaulted to `blog`; a site without Blog failed. 2.0.2 defaults to `page`.
- `varbase_ai_default` 2.x applies `varbase_ai_seo`, which ships strict config for `node.blog` and `node.page`: add a Blog type first on templates without one.
- Do not re-apply `drupal_cms_ai` later with a different `provider`: it rewrites the default providers.
- The recipe.yml description still says "OpenAI integration"; the default provider is amazee.ai.

## History

Base started January 2026; 1.0.0, 1.0.1, 1.0.2 (25 Oct 2026), 1.0.3 (27 Oct: Gemini #3633458, ElevenLabs #3633478, requires Default ~2 #3633094, functional tests #3633122). Default 1.0.x (since January 2025) is the Varbase 10.1.x line; 2.0.x started 25 Oct 2026 (#3633090), 2.0.0-alpha1 on 27 Oct.
