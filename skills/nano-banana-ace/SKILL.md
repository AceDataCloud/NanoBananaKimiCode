---
name: nano-banana-ace
description: Generate or edit Nano Banana image through Ace Data Cloud and retrieve the same task’s final result in Kimi Code. Use for explicit Nano Banana requests, not other media providers.
---

# Nano Banana by Ace Data Cloud

This plugin exposes only the Nano Banana workflow through the existing hosted Ace service. It does not change the conversation’s LLM provider.

Start by checking the connected tool schema. For setup inspection use `/mcp` and the tool schema; this plugin has no model-list tool and must not generate an image just to check connectivity. Never read, echo, or ask the user to paste an API Token into the conversation; it belongs in `ACEDATACLOUD_API_TOKEN` before Kimi starts.

For a new request, confirm the requested model/action, required inputs and current price are understood. Submit `nanobanana_generate_image` once only when the user has authorized the operation and its cost. Do not enable automatic generation retries or substitute a different model family.

Save the exact returned task_id. Use `nanobanana_get_task` to query that same task, observing server polling guidance. When it is still pending, explain that status and stop after a bounded check; let the user resume with the same ID. Never submit another generation to poll. Use nanobanana_get_task with the original task_id. Pending is not success; inspect terminal state and error before returning final image URLs. Do not silently switch to a different image family.

If the user supplies an existing task ID, query it directly without generating. If a request returns 401/403, explain key/scope or moderation errors without requesting secrets; for 429 wait and reduce concurrency; for 5xx/timeout inspect the existing task before any separately approved resubmission.

Setup and current service information: https://platform.acedata.cloud/documents/nano-banana-images?utm_source=agent_skill&utm_medium=referral&utm_campaign=evergreen&utm_content=nano_banana_kimi_readme_docs
