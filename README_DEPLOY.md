# Kiamora Coming Soon — deployment

This is a framework-free static page for `https://kiamora.in`. It does not require Node.js, Angular, Supabase, npm or `npx`.

## Files to copy

Copy **everything inside the `dist` folder** into the root of your GitHub repository. `index.html`, `styles.css`, `CNAME`, `.nojekyll`, and the `assets` folder must all be at repository root.

If your repository already contains the planning package, keep those Markdown files and folders. Add the files from `dist` alongside them.

## Publish using GitHub Pages

1. Commit and push the files to the `main` branch.
2. On GitHub, open the repository and select **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**.
4. Select branch **main**, folder **/(root)**, then select **Save**.
5. In **Custom domain**, enter `kiamora.in` and save it.
6. Configure your domain DNS using the exact values GitHub shows for the custom domain.
7. After GitHub confirms the DNS check, enable **Enforce HTTPS**.

Do not guess DNS values if your registrar shows different record types. Use the records displayed by GitHub Pages for your repository.

## Before going live

- Open `index.html` and confirm the WhatsApp number in the `wa.me` link.
- Double-click `index.html` to preview the page locally.
- Test the page on a phone and desktop.
- Test the **Enquire privately** button.

## Replace later with the Angular storefront

When the Angular storefront is ready, replace these temporary root files with the Angular production build. Keep the custom-domain configuration and `CNAME` file.
