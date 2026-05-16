# Florkin legal pages — GitHub Pages setup

This folder contains the privacy policy, terms of service, and support page
that the App Store requires Florkin to publish. Host them on GitHub Pages so
they live at stable HTTPS URLs.

## One-time setup

1. Create a new public repo on GitHub named **`florkin-legal`** under your
   account (`misaelgared`).
2. Push the contents of this folder (and only this folder — `privacy-policy.md`,
   `terms-of-service.md`, `support.md`, this README) to the root of that repo:

   ```bash
   cd legal
   git init
   git add .
   git commit -m "Florkin legal pages — v1"
   git branch -M main
   git remote add origin https://github.com/misaelgared/florkin-legal.git
   git push -u origin main
   ```

3. On GitHub, go to **florkin-legal → Settings → Pages**:
   - **Source**: Deploy from a branch
   - **Branch**: `main` / `/ (root)`
   - Save.

4. Rename the files at the served URLs by adding a `_config.yml` with a
   permalink scheme, OR simply update the URLs in
   `Florkin/Core/AppConstants.swift` to point at the `.html` versions Jekyll
   produces by default:

   ```
   https://misaelgared.github.io/florkin-legal/privacy-policy.html
   https://misaelgared.github.io/florkin-legal/terms-of-service.html
   https://misaelgared.github.io/florkin-legal/support.html
   ```

   The constants in `AppConstants.swift` already point at the clean
   `/privacy`, `/terms`, `/support` paths — easiest to add a `_config.yml`
   like the snippet below so those paths render the right markdown.

   ```yaml
   # _config.yml
   title: Florkin
   theme: jekyll-theme-minimal
   permalink: /:title

   defaults:
     - scope:
         path: ""
       values:
         layout: default
   ```

   Then commit and push; GitHub rebuilds the Pages site automatically.

5. Wait ~1 minute, then verify all three URLs are live:

   - https://misaelgared.github.io/florkin-legal/privacy
   - https://misaelgared.github.io/florkin-legal/terms
   - https://misaelgared.github.io/florkin-legal/support

That's it — copy those URLs into App Store Connect's privacy and support URL
fields, and Florkin will deep-link to them from Settings.

## Updating after launch

The "Last updated" date at the top of each page is the only thing reviewers
look at when checking for material changes. Bump it whenever you change the
substance of either policy.
