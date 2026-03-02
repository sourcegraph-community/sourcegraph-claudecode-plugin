---
name: sg-search
description: Search Sourcegraph using natural language or keyword queries.
---

# Sourcegraph Search

Run a Sourcegraph search using text provided after `/sourcegraph:sg-search`.

If the query is natural language, use `nls_search` first.
If it looks like Sourcegraph query syntax or regex, use `keyword_search`.

After searching:

1. Summarize the most relevant matches.
2. Include repositories and files for the top hits.
3. Suggest one to three refined follow-up queries when results are broad.
