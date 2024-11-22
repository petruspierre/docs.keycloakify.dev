# Editing or Removing Keycloak Styles

{% hint style="info" %}
For CSS Level Customization Keycloak provides a standardized way of customization through the use of _theme.properties._ This way Keycloak provides a basic theme.\
Follow this tutorial if you want to port an existing theme or develop a new theme based on the Keycloak Base Theme and **without having to overwrite the pages**
{% endhint %}

## Styling a Keycloak Class with CSS

Upon inspecting the DOM in your login theme you can see that an element usually has a class starting with _kc_ in this case _kcFormHeaderClass._ The succeeding class _login-pf-header_ represents Patternfly styles and is mapped by the _kcFormHeaderClass._

<figure><img src="../../../.gitbook/assets/header_class_login.JPG" alt="" width="563"><figcaption><p>The header element has multiple classes</p></figcaption></figure>

If you want to add a red border to the header class you can do so by directly overwriting the Keycloak CSS class in your _styles.css_

{% code title="styles.css" %}
```css
.kcFormHeaderClass {
    border: 3px solid red;
}
```
{% endcode %}

<figure><img src="../../../.gitbook/assets/grafik (1).png" alt="" width="467"><figcaption><p>Login Header with red border</p></figcaption></figure>

## Styling a Keycloak Class with Custom Class Bindings

There are mutliple scenarios where you want to bind custom classes:

1. Applying Patternfly, Tailwind or Bootstrap classes
2. Applying your own CSS Classes

Let's say that we would like to add a red border to the header element of the login page but with a class _red-border_ instead of applying the style directly.

You can define a CSS class and bind it using the classes array in your KcPage. You can also bind any other class from e. g. Patternfly , Tailwind or Boostrap&#x20;

{% code title="styles.css" %}
```css
.red-border {
    border: 3px solid red;
}
```
{% endcode %}

{% code title="KcPage.tsx/ KcPage.ts" %}
```tsx
const classes = {
  kcFormHeaderClass: "login-pf-header red-border",
} satisfies { [key in ClassKey]?: string };
```
{% endcode %}

<figure><img src="../../../.gitbook/assets/grafik (1).png" alt="" width="467"><figcaption><p>Login Header with red border</p></figcaption></figure>

## Removing a Default Style

Keycloakify enables you to use this Keycloak concept to easily edit the default styles. For example let's remove the _login-pf-header_ class:

{% tabs %}
{% tab title="React" %}
<pre class="language-tsx" data-title="src/login/KcPage.tsx"><code class="lang-tsx">const classes = {
<strong>    kcFormHeaderClass: ""
</strong>} satisfies { [key in ClassKey]?: string };
</code></pre>
{% endtab %}

{% tab title="Angular" %}
{% code title=" src/login/KcPage.ts" %}
```typescript
const classes = {
    kcFormHeaderClass: ""
} satisfies { [key in ClassKey]?: string };
```
{% endcode %}
{% endtab %}
{% endtabs %}

We can see that now, the header element has no other class binding than _kcFormHeaderClass_ as we removed the _login-pf-header_ class. As a result the header text is now aligned to the left.

<figure><img src="../../../.gitbook/assets/no_header_class_login (1).JPG" alt="" width="563"><figcaption><p>Now the header has only one class</p></figcaption></figure>



## Removing all Default Styles

Maybe you'd prefer to remove all default styles at once you can do that by setting _doUseDefaultCss_ to false. This option is also available to set on a per page basis.

{% tabs %}
{% tab title="React" %}
<pre class="language-tsx" data-title="src/login/KcPages.tsx"><code class="lang-tsx">export default function KcPage(props: { kcContext: KcContext }) {

    return (
        &#x3C;Suspense>
            {(() => {
                switch (kcContext.pageId) {
                    default:
                        return (
                            &#x3C;DefaultPage
                                kcContext={kcContext}
                                i18n={i18n}
                                classes={classes}
                                Template={Template}
<strong>                                doUseDefaultCss={false}
</strong>                                UserProfileFormFields={UserProfileFormFields}
                                doMakeUserConfirmPassword={doMakeUserConfirmPassword}
                            />
                        );
                }
            })()}
        &#x3C;/Suspense>
    );
}
</code></pre>
{% endtab %}

{% tab title="Angular" %}
<pre class="language-typescript" data-title="src/login/KcPage.ts"><code class="lang-typescript">const classes = {} satisfies { [key in ClassKey]?: string };
<strong>const doUseDefaultCss = false;
</strong>const doMakeUserConfirmPassword = true;

export async function getKcPage(pageId: KcContext['pageId']): Promise&#x3C;KcPage> {
  switch (pageId) {
    default:
      return {
        PageComponent: await getDefaultPageComponent(pageId),
        TemplateComponent,
        UserProfileFormFieldsComponent,
        doMakeUserConfirmPassword,
        doUseDefaultCss,
        classes,
      };
  }
}

</code></pre>


{% endtab %}
{% endtabs %}

However be aware that re-styling everything involves quite a bit of work:

<figure><img src="../../../.gitbook/assets/image (31).png" alt="" width="375"><figcaption><p>The login page with doUseDefaultCss set to false</p></figcaption></figure>

