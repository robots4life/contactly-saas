### 1.1 - SvelteKit Project Setup

https://courses.huntabyte.com/view/courses/modern-saas/1887088-module-1-project-setup/6175530-1-1-sveltekit-project-setup

https://github.com/huntabyte/modern-saas/blob/starter-code/.prettierrc#L6 has `prettier-plugin-tailwindcss` but https://github.com/huntabyte/modern-saas/blob/starter-code/package.json does not have `prettier-plugin-tailwindcss`.

After `git clone --single-branch --branch starter-code https://github.com/huntabyte/modern-saas.git` going to `src/lib/index.ts` and writing some JS, on save, prettier does not format it.

```bash
["INFO" - 5:15:35 PM] Formatting file:///.../modern-saas/src/lib/index.ts
["INFO" - 5:15:35 PM] Using config file at '/.../modern-saas/.prettierrc'
```

Now, when I do `pnpm install prettier-plugin-tailwindcss` it complains about a version mismtach to `prettier`.

When I remove `prettier-plugin-tailwindcss` from `.prettierrc` like so, it works.

```json
{
	"useTabs": true,
	"singleQuote": false,
	"trailingComma": "none",
	"printWidth": 100,
	"plugins": ["prettier-plugin-svelte"],
	"pluginSearchDirs": false,
	"overrides": [
		{
			"files": "*.svelte",
			"options": {
				"parser": "svelte",
				"svelteIndentScriptAndStyle": true,
				"svelteStrictMode": false,
				"svelteSortOrder": "scripts-markup-styles-options"
			}
		}
	],
	"bracketSameLine": true
}
```

@huntabyte please tell me how to exactly install `pnpm install prettier-plugin-tailwindcss` with the exact version needed to that prettier and `prettier-plugin-svelte` as well **`prettier-plugin-tailwindcss`** work nicely together, thank you.
