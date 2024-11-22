---
icon: rocket-launch
---

# Quick Start

Keycloakify is a tool that enables to create keycloak themes for customizing of the look and feel of Keycloak's user-facing pages. You can preview these pages here:

{% embed url="https://storybook.keycloakify.dev/" %}
Preview your Keycloakify Theme with Storybook
{% endembed %}

### Why would I chose a third party tool over the theming system [featured by Keycloak](https://www.keycloak.org/docs/latest/server\_development/#\_themes)?

* Keycloakify lets you use modern frontend technology: **TypeScript**, **React**, **Angular** and **any styling solution or component library** you'd like, such as **Tailwind**, **MUI**, **shadcn/ui**, or just **plain CSS**.&#x20;
* Keycloakify makes it very easy to test your theme [inside](basics/testing-your-theme/in-a-keycloak-docker-container.md) and [outside](basics/testing-your-theme/in-storybook.md) Keycloak with hot reloading enabled.
* Keycloakify bundles the theme for you into a JAR that you can simply [import into Keycloak](basics/importing-your-theme-in-keycloak.md).
* The Keycloak themes generated with Keycloakify are downside compatible with all Keycloak Versions down to 11
* Keycloakify themes implement **real-time frontend validation** out of the box. For example, when a user chooses a password that is too weak, they see the feedback message like _"_the password must be at least 12 character long_"_ immediately and not after they have pressed the submit button.
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

For starters you can add a story of a page you want to test and start a locale storybook. Before that you need to copy the patternfly resources for locale development

```bash
npx keycloakify copy-keycloak-resources-to-public
npx keycloakify add-story
npm run storybook
```

Now you should be able to see the login page with all its test cases:

<figure><img src=".gitbook/assets/grafik (2).png" alt=""><figcaption></figcaption></figure>

### Customize the Login Page CSS

Keycloakify gives you many options on how to customize a theme. For the quickstart overwrite a css style of a Keycloak class:

{% code title="styles.css" %}
```css
.kcFormHeaderClass {
    border: 3px solid red;
}
```
{% endcode %}

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
