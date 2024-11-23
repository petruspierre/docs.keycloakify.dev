# Angular Workspace

{% hint style="info" %}
This tutorial requires some experience with Angular. The steps are straight forward but they might require some configuration depending on your project.
{% endhint %}

## Integrating Keycloakify into an Angular Workspace

Let's assume you have a monorepo project where sub applications are stored in the **projects/** directory.

Next up you want to repatriate the Keycloakify Starter template sources.\
Only copy over the src and .storybook directory.

```bash
cd my-workspace
git clone https://github.com/keycloakify/keycloakify-starter-angular tmp
mv tmp/src projects/keycloak-theme
mv tmp/extra-webpack.config.js tmp/index-html-transform.js
rm -rf tmp
```

#### Adjust the `extra-webpack.config.js` File

Edit the highlighted path in `extra-webpack.config.js` file to match the following configuration:

<pre class="language-javascript" data-title="extra-webpack.config.js"><code class="lang-javascript">import path from 'node:path';
import MiniCssExtractPlugin from 'mini-css-extract-plugin';

export default {
  entry: './projects/keycloakify-theme/src/main.ts',
  output: {
<strong>    path: path.resolve(import.meta.dirname, '../../dist/keycloakify-theme/static/js/'),
</strong>    publicPath: 'auto',
  },
  plugins: [
    new MiniCssExtractPlugin({
      filename: '../css/[name].[contenthash].css',
    }),
  ],
};
</code></pre>

after this, your project structure should look like the following:

```
my-workspace/

│
├── projects/
│   └── keycloakify-theme/
│       ├── src/
│       ├── index-html-transform
│       ├── extra-webpack.js
│       ├── tsconfig.app.json
│       └── tsconfig.spec.json
│
├── angular.json
└── package.json

```

### Update `package.json` with Keycloakify Configuration

Ensure the following lines are present in your workspace's `package.json`:

<pre class="language-json" data-title="package.json"><code class="lang-json">{
  "name": "my-workspace",
  "version": "0.0.0",
<strong>  "type": "module",
</strong>  "scripts": {
    ...
<strong>    "build-keycloak-theme": "ng build keycloakify-theme &#x26;&#x26; npx keycloakify build --project projects/keycloakify-theme",
</strong>    ...
  },
<strong>  "keycloakify": {
</strong><strong>    "accountThemeImplementation": "none",
</strong><strong>    "projectBuildDirPath": "dist/keycloakify-theme",
</strong><strong>    "staticDirPathInProjectBuildDirPath": "static",
</strong><strong>    "publicDirPath": "public"
</strong><strong>  },
</strong>  "dependencies": {
    ...
<strong>    "keycloakify": "^11.3.18",
</strong><strong>    "@keycloakify/angular": "0.1.4"
</strong>    ...
  },
  "devDependencies": {
    ...
<strong>    "@angular-builders/custom-webpack": "^18.0.0",
</strong>    ...
  }
}
</code></pre>

### Add the Keycloakify Project to `angular.json`

To integrate the **Keycloakify** project into your workspace, update the `angular.json` file by adding an entry to the `projects` section. Below is an example configuration. Important lines that may require customization based on your project’s requirements are highlighted:

<pre class="language-json" data-title="angular.json"><code class="lang-json">"keycloakify-theme": {
  "projectType": "application",
  "schematics": {
    "@schematics/angular:component": {
      "changeDetection": "OnPush",
      "style": "css",
      "standalone": true
    }
  },
<strong>  "root": "projects/keycloakify-theme",
</strong><strong>  "sourceRoot": "projects/keycloakify-theme/src",
</strong>  
  "prefix": "kc",
  "architect": {
    "build": {
        "builder": "@angular-builders/custom-webpack:browser",
        "options": {
          "inlineStyleLanguage": "scss",
<strong>            "outputPath": "dist/keycloakify-theme",
</strong><strong>            "index": "projects/keycloakify-theme/src/index.html",
</strong><strong>            "main": "projects/keycloakify-theme/src/main.ts",
</strong><strong>            "tsConfig": "projects/keycloakify-theme/tsconfig.app.json"
</strong>        },

        "configurations": {
          "production": {
              "optimization": true,
<strong>              "indexTransform": "projects/keycloakify-theme/index-html-transform.js",
</strong>              "sourceMap": false,
              "customWebpackConfig": {
<strong>                  "path": "projects/keycloakify-theme/extra-webpack.config.js",
</strong>                  "mergeRules": {
                      "output": "replace",
                      "entry": "replace",
                      "plugins": "append"
                  }
              }
          },
          "development": {
            "assets": [
              {
                "glob": "**/*",
                "input": "./public"
              }
            ],
              "buildOptimizer": false,
              "optimization": false,
              "sourceMap": true,
              "namedChunks": true
          }
      },
      "defaultConfiguration": "production"
  },
    "serve": {
      "builder": "@angular-builders/custom-webpack:dev-server",
      "options": {
        "buildTarget": "keycloakify-theme:build"
      },
      "configurations": {
        "production": {
          "buildTarget": "keycloakify-theme:build:production"
        },
        "development": {
          "buildTarget": "keycloakify-theme:build:development"
        }
      },
      "defaultConfiguration": "development"
    }
  }
},
</code></pre>

## Use Keycloakify

The application should now be good to go. Make sure that whenever you run a `npx keycloakify` command in your workspace root you add the path to your keycloakify project like this:\
`npx keycloakify build --project projects/keycloakify-theme`

