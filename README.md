# 👨‍💻 Quick start

Keycloakify is a tool that enables customization of the look and feel of Keycloak's user-facing pages. You can preview these pages here:&#x20;

{% embed url="https://storybook.keycloakify.dev/" %}

Why do I need Keycloakify in the first place? Why can't I just implement the default theming system provided by Keycloak?

* Keycloakify lets you use modern frontend technology: TypeScript, React, and any styling solution or component library you'd like, such as TailwindCSS, MUI, ShadeCN/UI, or just plain CSS modules. With the base theming system you have to write [FreeMarker](https://freemarker.apache.org/index.html) and integrating frontend technologies into a Java Stack isn't straight forward.
* Keycloakify makes it very easy to test your theme inside and outside Keycloak with hot reloading enabled.
* Keycloakify bundles the theme for you into a JAR that you can simply import into Keycloak.
* The Keycloak themes generated with Keycloakify are compatible with all Keycloak versions down to v11, by oposition to regular themes that must be updated to target a specific Keycloak version.
* Keycloakify themes implement real-time frontend validation out of the box. For example, when a user chooses a password that is too weak, they see the feedback immediately and not after they have pressed the submit button.
* Keycloakify is well-documented, well-maintained, and you're welcome to join [our Discord](https://discord.gg/kYFZG7fQmn) channel if you're having difficulties.

Start playing with the starter project now and come back here in a few minutes to learn more!

{% embed url="https://github.com/codegouvfr/keycloakify-starter" %}
