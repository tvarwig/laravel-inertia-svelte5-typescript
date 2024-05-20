# Laravel Inertia Svelte 5 TypeScript

## Description

This repository is a boilerplate project integrating Laravel, Inertia.js, Svelte 5, and TypeScript, designed to provide a seamless and efficient development environment for building modern, reactive web applications.

## Features

- **Laravel**: Robust backend framework for building web applications with elegant syntax.
- **Inertia.js**: Eliminates the need for client-side routing, providing a modern single-page application experience without complex SPA libraries.
- **Svelte 5**: A radical new approach to building user interfaces with a focus on performance and simplicity.
- **TypeScript**: Enhances JavaScript with static typing, improving developer experience and code quality.
- **Tailwind CSS**: Utility-first CSS framework for rapid UI development.
- **Vite**: Next-generation frontend tooling for fast development and hot module replacement.

## Getting Started

### Using

- PHP >= 8.3
- Node.js >= 20
- Composer

### Issues
- "svelte": "^5.0.0-next.136" in package.json. `npm install` doesn't always work with this line in package.json. You may need to delete this line and manually install svelte@next

### Changes from Docs

```bash
npm install svelte@next @sveltejs/vite-plugin-svelte @inertiajs/svelte
```

```javascript
// creted svelte.config.js
import { vitePreprocess } from '@sveltejs/vite-plugin-svelte';

export default {
preprocess: [vitePreprocess()]
};
```

```javascript
// vite.config.js
import { defineConfig } from "vite";
import laravel from "laravel-vite-plugin";
import { svelte } from "@sveltejs/vite-plugin-svelte";  // added this line

export default defineConfig({
    plugins: [
        laravel({
            input: ["resources/css/app.css", "resources/js/app.js"],
            refresh: true,
        }), 
      svelte({}), // added this line
    ],
});
```

```javascript
// sresources/js/app.js
import { createInertiaApp } from '@inertiajs/svelte'
import {mount} from "svelte";

createInertiaApp({
  resolve: name => {
      const pages = import.meta.glob('./Pages/**/*.svelte')
      return pages[`./Pages/${name}.svelte`]()
  },
  setup({ el, App, props }) {
      mount(App, { target: el}, props)
  },
})
```

```svelte
// resources/views/js/Pages/Welcome.svelte
<script lang="ts">
    let { name }: { name: string } = $props();
</script>

<main>
    <h1>Welcome back, {name}! - We are using Svelte 5 in Inertia.js with Typescript</h1>
</main>

```
