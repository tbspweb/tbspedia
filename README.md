# TBSPedia

TBSPedia is the Tahoe Backcountry Ski Patrol's reference manual. It used to be
a MediaWiki site. It is now a set of Markdown pages that admins edit directly
on GitHub. GitHub Pages publishes the pages under the main TBSP site at
`/tbspedia/`.

## Who can edit

Only **tbspweb organization admins** (and anyone they add as collaborators on
this repository) can change pages. Visitors to the website can read the pages,
but they can't edit them, and there are no comment or talk pages.

> **Every page here is public.** Anyone on the internet can read it, and so can
> search engines. This repository is also public on GitHub, so anyone can read
> its full edit history too, including deleted text.
> Never add passwords, gate or lock codes, share-link passwords, private
> phone numbers, home addresses, or personal email addresses. Link to
> Beacon or Confluence for anything that's members-only.

## Edit a page (in your browser)

1. Open the page's `.md` file in this repository. For example,
   `Chapter_05__Communications.md`.
2. Click the pencil icon (✏️) at the top right.
3. Make your changes. Click **Preview** to check them.
4. Click **Commit changes...**, write a short note about what you changed, and
   click **Commit changes** again.
5. The site updates within about two minutes. You can follow progress in the
   **Actions** tab: green means done, red means the build failed (the old
   version stays up).

## Add a new page

1. On the repository's main page, click **Add file** → **Create new file**.
2. Name the file using words joined by underscores, ending in `.md`, for
   example `Avalanche_Beacon_Practice.md`. The page will be published at
   `/tbspedia/Avalanche_Beacon_Practice`.
3. Start the file with this block (keep the `---` lines):

   ```
   ---
   layout: default
   title: Avalanche Beacon Practice
   ---

   # Avalanche Beacon Practice

   Page text goes here.
   ```

4. Commit it, then link to it from `index.md` (the TBSPedia home page) so
   people can find it.

## Linking and images

- To link to another TBSPedia page, use its file name:
  `[Radio Operation](Appendix_I__Radio_Operation.md)`.
- Images live in the `images/` folder. To add one, open that folder, click
  **Add file** → **Upload files**, and use names without spaces. To show an
  image on a page, add `![What the image shows](images/Prusik.png)`.

## Retiring a page

Move outdated pages into `archive/` rather than deleting them. **Pages in
`archive/` are still published and public.** If an old page contains personal
information, delete the page or remove that information instead.
