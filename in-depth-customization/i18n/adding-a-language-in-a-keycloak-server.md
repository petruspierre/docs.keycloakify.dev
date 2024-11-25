# Adding a Language in a Keycloak Server

In the Keycloak Admin Console you can enable localization by selecting a set of language that you wish to support. After that you should be able to select a language in your Login.&#x20;

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>Languages in Keycloak Server</p></figcaption></figure>

{% hint style="info" %}
The language that you want to support isn't in the default set? You can add support for it with Keycloakify. [See how](adding-support-for-extra-languages.md).
{% endhint %}

<figure><img src="../../.gitbook/assets/image (6).png" alt="" width="375"><figcaption></figcaption></figure>

{% hint style="success" %}
You shouldn't rely on the language select to let your users select their language. &#x20;

Infact, I encourage you to hide or remove it. &#x20;

What you should do instead is, when redirecting your user from your application to your Keycloak login page, add an extra query param to let Keycloak know in what language the page should be rendered. &#x20;

The parameter to add is ?ui\_locales=fr (Example if we want the UI to be in French). &#x20;

See [oidc-spa documentation](https://docs.oidc-spa.dev/documentation/usage) for more info on how to provide this parameter. (You can do the same if you use keycloak-js or NextAuth)
{% endhint %}
