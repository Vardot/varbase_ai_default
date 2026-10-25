[![Varbase](https://raw.githubusercontent.com/Vardot/varbase/11.0.x/images/varbase-logo.png)](https://www.drupal.org/project/varbase)

# Varbase AI Default

Applies Varbase AI Base and every Varbase AI recipe in one step, with MariaDB as the vector database. For demos, and for sites that want the full Varbase AI stack.

## What it applies

* [Varbase AI Base](https://www.drupal.org/project/varbase_ai_base)
* [Varbase AI VDB: MariaDB](https://www.drupal.org/project/varbase_ai_vdb_mariadb)
* [Varbase AI Search Base](https://www.drupal.org/project/varbase_ai_search_base)
* [Varbase AI Chatbot Base](https://www.drupal.org/project/varbase_ai_chatbot_base)
* [Varbase AI Answers Base](https://www.drupal.org/project/varbase_ai_answers_base)
* [Varbase AI Content Operations Base](https://www.drupal.org/project/varbase_ai_content_operations_base)
* [Varbase AI MCP Server Base](https://www.drupal.org/project/varbase_ai_mcp_server_base)
* [Varbase AI Readable Base](https://www.drupal.org/project/varbase_ai_readable_base)
* [Varbase AI SEO](https://www.drupal.org/project/varbase_ai_seo)
* [Varbase AI Media Base](https://www.drupal.org/project/varbase_ai_media_base)
* [Varbase AI Figma Base](https://www.drupal.org/project/varbase_ai_figma_base)

## Inputs

Applied from Project Browser or the recipe form, it asks for the inputs of every recipe it applies: the AI provider and its API key, the editor for the AI assistant, the content type and fields for AI tagging, and the Figma access token. Leave an input as it is to keep its default.

From Drush, pass any of them with `--input`:
```
drush recipe ../recipes/varbase_ai_default \
  --input=drupal_cms_ai.provider=openai \
  --input=drupal_cms_ai.openai_api_key=YOUR_KEY \
  --input=varbase_ai_taxonomy_tagging.content_type=news
```

MariaDB 11.7 or later is needed for the vector database.

## Documentation

Read the [Varbase AI Recipes](https://docs.varbase.vardot.com/developers/understanding-varbase/varbase-ai-recipes) documentation on the Varbase docs site.

## Installation

Varbase AI Default comes with Varbase AI Base, which requires it and every recipe it applies:
```
composer require drupal/varbase_ai_base:~1
```

Change directory to `/web` or `/docroot`

Run the Drupal recipe bash script:
```
bash core/scripts/drupal recipe ../recipes/varbase_ai_default
```

or

Run the Drush recipe command:
```
drush recipe ../recipes/varbase_ai_default
```
