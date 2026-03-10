---
title: "mdchart Playground in Hugo"
date: 2026-03-10T07:35:00+05:30
draft: false
tags: ["hugo", "mdchart", "charts"]
description: "Interactive chart DSL playground backed by FastAPI"
---

I deployed a FastAPI backend that renders my chart DSL into matplotlib PNGs. This page embeds a playground shortcode that calls the API directly from the browser.

{{< mdchart-playground />}}

## Usage in any post

1. Make sure `params.mdchartApiURL` is set in `config.yml`.
2. Add the shortcode:

```markdown
{{</* mdchart-playground />}}
```

You can override the API URL per instance:

```markdown
{{</* mdchart-playground api_url="https://your-api-host.com" />}}
```

You can also pass initial DSL as inner content:

```markdown
{{</* mdchart-playground */>}}
type = line;
x = week;
y = users;
data = [W1:22, W2:34, W3:29];
{{</* /mdchart-playground */>}}
```
