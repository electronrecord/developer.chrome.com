---
layout: 'layouts/doc-post.njk'
title: Add an API
description: 'Add an API to the reference area.'
date: 2020-12-17
---

## Add an API

To add a reference page for a Chrome API, create a folder and `index.md` file inside
`site/en/docs/extensions/reference/`. The folder name doesn't directly relate to the API
itself—control which API is rendered via frontmatter like this:

```md
---
api: browserAction
---

Something about this API. This text is completely optional. If you don't want to write anything,
then you should include a comment like <!-- This is intentionally empty -->.
```

The API name is assumed to be under "chrome.apiName". If you are documenting an API like
"chrome.input.ime", then by convention, the folder name should be "input_ime" but the API in your
frontmatter shold still be `api: input.ime`.

The existence of this page will cause the API itself to be displayed in the
[top-level reference page][1]. If it's a Chrome Apps-only API, it will appear at the very bottom
of that page, rather than in Stable, Beta or Dev.

## API Source

The API reference is generated via the published APIs in [chrome-types on NPM][2]. It's possible
for that dependency to get out-of-date; if you're trying to document a new API, take these steps:

- Run `npm install chrome-types` to ensure that latest version is available.
- Run `npm run types` to build our fast internal reprensetation of the TypeScript definition files (this normally happens on checkout, but since you've updated the types, it needs a re-run)

### Updating APIs

Our TypeScript definition files are generated by by running "npm deploy" from within
[the npm subfolder][3] of that repo, which will check out the right parts of Chromium and
automatically build the TypeScript definition files. (At some point, this will happen automatically
but as of December 2020, it's still a manual step.)

[1]: /docs/extensions/reference/
[2]: https://www.npmjs.com/package/chrome-types
[3]: https://github.com/GoogleChrome/chrome-types/tree/main/npm