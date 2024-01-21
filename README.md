# my-ex-github-pages-vue

my excercise for deploying a vue application to github pages

## OPtions:

There seems mainly 2 ways to publish a Vue.js application on GitHub Pages.

- Option1: Build into `docs` directory & Setting Pages

  This is simple and quick.

- Option2: Build into `dist` directory & deploy with GitHub Workflow

  This needs just a little complicated settings and more time to publish.

## Option1 Steps:

1. Create a Vue.js application on local

- example source:`src/App.vue`

    ```Vue
    <script setup>
    import {ref} from 'vue'

    const text = ref('')

    function onInput(e) {
    text.value = e.target.value
    }
    </script>

    <template>
    <input :value="text" v-on:input="onInput" placeholder="Type here">
    <p>{{ text }}</p>
    </template>
    ```

2. Edit vite.config.js on local

    Add following setting, if you publish to repository pages.

    ```
    base: './',
    build: {
        outDir: 'docs'
    }
    ```

    See more [Deploying a Static Site | Vite](https://vitejs.dev/guide/static-deploy.html)

    For example:

    ```javascript
    import { fileURLToPath, URL } from 'node:url'

    import { defineConfig } from 'vite'
    import vue from '@vitejs/plugin-vue'

    // https://vitejs.dev/config/
    export default defineConfig({
    plugins: [
        vue(),
    ],
    resolve: {
        alias: {
        '@': fileURLToPath(new URL('./src', import.meta.url))
        }
    },
    base: './',
    build: {
        outDir: 'docs'
    }
    })
    ```

3. Build on local

    ```bash
    npm run build
    ```

4. commit & push to the GitHub Public Repository

5. Change the settings of the applicable GitHub repository.

    - Open `Settings` tab on the GitHub Repository.
    - Choose `Pages` on the side menu.
    - Select `Deploy from a Branch` from the `Source` pull down menu in `Build and deployment` section.
    - Select `main` from the `Branch` pull down menu.
    - Select `/docs` from the `Select folder` pull down menu, next to the `Branch` menu.
    - Click `Save` button next to the `Select folder` pull down menu.

6. View the GitHub Pages on your browser

    The url format is:
    
    https://[username].github.io/[repositoryname]/

## Option2 Steps:

1. Create a Vue.js application on local

2. Edit vite.config.js on local

    Add following setting, if you publish to repository pages.

    ```
    base: '/<REPO>/'
    ```

    See more [Deploying a Static Site | Vite](https://vitejs.dev/guide/static-deploy.html)

    For example:

    ```javascript
    import { fileURLToPath, URL } from 'node:url'

    import { defineConfig } from 'vite'
    import vue from '@vitejs/plugin-vue'

    // https://vitejs.dev/config/
    export default defineConfig({
    plugins: [
        vue(),
    ],
    resolve: {
        alias: {
        '@': fileURLToPath(new URL('./src', import.meta.url))
        }
    },
    base: '/my-ex-github-pages-vue/'
    })
    ```

3. Build on local

    ```bash
    npm run build
    ```

4. commit & push to the GitHub Public Repository

5. Change the settings of the applicable GitHub repository.

    - Open `Settings` tab on the GitHub Repository.
    - Choose `Pages` on the side menu.
    - Select `GitHub Actions` from the `Source` pull down menu in `Build and deployment` section.
    - Click `Cofigure` button of `Static HTML` workflow.
    - Modify the value of `path` in the fourth line from the end to `./dist`.
    - Click `Commit Changes` button.
    - Check `Create a new branch ...` and click `Propose changes` button
    - Merge the new branch to the main branch.
    - Check result of `Actions`.

6. View the GitHub Pages on your browser

***

*Document Created: 2024/01/20*

*Document Updated: 2024/01/21*

Copyright 2024 macocci7
