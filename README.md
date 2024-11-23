---
icon: rocket-launch
---

# Quick Start

Keycloakify is a tool that enables to create keycloak themes for customizing of the look and feel of Keycloak's user-facing pages. You can preview these pages here:

{% embed url="https://storybook.keycloakify.dev/" %}
Preview your Keycloakify Theme with Storybook
{% endembed %}

### Why would I chose a third party tool over the theming system [featured by Keycloak](https://www.keycloak.org/docs/latest/server_development/#_themes)?

* Keycloakify lets you use modern frontend technology: **TypeScript**, **React**, **Angular** and **any styling solution or component library** you'd like, such as **Tailwind**, **MUI**, **shadcn/ui**, or just **plain CSS**.&#x20;
* Keycloakify makes it very easy to test your theme [inside](basics/testing-your-theme/in-a-keycloak-docker-container.md) and [outside](basics/testing-your-theme/in-storybook.md) Keycloak with hot reloading enabled.
* Keycloakify bundles the theme for you into a JAR that you can simply [import into Keycloak](basics/importing-your-theme-in-keycloak.md).
* The Keycloak themes generated with Keycloakify are downside compatible with all Keycloak Versions down to 11
* Keycloakify themes implement **real-time frontend validation** out of the box. For example, when a user chooses a password that is too weak, they see the feedback message like _"_&#x74;he password must be at least 12 character lon&#x67;_"_ immediately and not after they have pressed the submit button.
* We're here to help! Either via [our Discord](https://discord.gg/kYFZG7fQmn) channel or [GitHub issues](https://github.com/keycloakify/keycloakify/issues/new).

### Clone Repository

{% tabs %}
{% tab title="React" %}
First thing you want to do is to fork/clone the Keycloakify Vite[^1] starter template and install the dependencies

```bash
git clone https://github.com/keycloakify/keycloakify-starter
cd keycloakify-starter
yarn
```
{% endtab %}

{% tab title="Angular" %}
First thing you want to do is to fork/clone the [Keycloakify Angular ](#user-content-fn-2)[^2]starter template.

```bash
git clone https://github.com/keycloakify/keycloakify-starter-angular
cd keycloakify-starter-angular
yarn
```
{% endtab %}
{% endtabs %}

### Spin up the Theme Outside Keycloak

For starters you can add a story of a page you want to test and start a locale Storybook[^3].&#x20;

```bash
npx keycloakify add-story # Select login.ftl (for example)
npm run storybook 
```

You should now be able to see the login pages in different scenarios:

<figure><img src=".gitbook/assets/grafik (2).png" alt=""><figcaption></figcaption></figure>

### Customize the Login Page CSS

Keycloakify gives you many options on how to customize a theme but let's just start by adding a custom CSS rule. \


{% tabs %}
{% tab title="React" %}
Create this file: &#x20;

{% code title="src/login/main.css" %}
```css
.kcFormHeaderClass {
    border: 3px solid red;
}
```
{% endcode %}

The import it by adding this line at the top of the KcPage.tsx file:&#x20;

<pre class="language-tsx" data-title="src/login/KcPage.tsx"><code class="lang-tsx"><strong>import "./main.css";
</strong></code></pre>
{% endtab %}

{% tab title="Angular" %}
{% code title="src/styles.css" %}
```css
.kcFormHeaderClass {
    border: 3px solid red;
}
```
{% endcode %}


{% endtab %}
{% endtabs %}

<figure><img src=".gitbook/assets/grafik (3).png" alt=""><figcaption></figcaption></figure>

There are several methods for customizing your theme. We recommend using a different Base Theme for example with MUI or Angular Material. Also you can test your theme in a Keycloak Container:

{% content-ref url="basics/testing-your-theme/" %}
[testing-your-theme](basics/testing-your-theme/)
{% endcontent-ref %}

{% content-ref url="in-depth-customization/customization-strategies/" %}
[customization-strategies](in-depth-customization/customization-strategies/)
{% endcontent-ref %}

[^1]: There's also a Webpack based starter that you can find [here](https://github.com/keycloakify/keycloakify-starter-webpack).

[^2]: There is also a Vite based starter:\
    [https://github.com/keycloakify/keycloakify-starter-angular-vite](https://github.com/keycloakify/keycloakify-starter-angular-vite)

[^3]: [Storybook](https://storybook.js.org/) is a tool that allows you to develop UI components in isolation. It is set up in the Keycloakify starter repos because it provides an good developer experience and makes it easy to quickly preview the different pages of your theme.
