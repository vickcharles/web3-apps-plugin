---
description: Deploy the website to a permanent vibe3.link subdomain
allowed-tools: Bash, Write, mcp__vibe3-mcp__update_deployment_info, mcp__vibe3-mcp__set_preview_image, mcp__playwright__browser_navigate, mcp__playwright__browser_take_screenshot, mcp__playwright__browser_close
---

Deploy this website to Vercel with a permanent subdomain.

## Steps:

1. Generate a URL-friendly slug (2-4 words, lowercase, hyphenated) based on what was built.
   The slug must be unique and descriptive. Examples: "ai-weather-app", "portfolio-dark", "recipe-finder"

2. Run the Vercel deploy command:
   ```bash
   vercel deploy --prod --public --token=$VERCEL_ACCESS_TOKEN --yes --force --scope=$VERCEL_TEAM_ID
   ```

3. After deploy succeeds, set the custom domain alias:
   ```bash
   vercel alias set <deployment-url> <slug>.vibe3.link --token=$VERCEL_ACCESS_TOKEN --scope=$VERCEL_TEAM_ID
   ```

4. **If a dev server is running** at `http://localhost:3000`, take a screenshot:
   - Navigate to `http://localhost:3000` using `browser_navigate`
   - Wait a moment for the page to fully render
   - Take a screenshot using `browser_take_screenshot` and save it to `/tmp/preview.png`
   - Close the browser using `browser_close`
   If no dev server is available (e.g., during initial generation), skip this step entirely.

5. Call the `update_deployment_info` MCP tool with:
   - `url`: `https://<slug>.vibe3.link`
   - `slug`: `<slug>`

6. If a screenshot was taken in step 4, call the `set_preview_image` MCP tool with:
   - `screenshot_path`: `/tmp/preview.png`
   Otherwise, skip this step.
