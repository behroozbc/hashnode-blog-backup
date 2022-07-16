## Angular PWA Internationalization

## What is Internationalization (i18n)?

*Internationalization*, sometimes referenced as i18n, is the process of designing and preparing your project for use in different locales worldwide. Localization is the process of building versions of your project for other locales.
## What is Angular proposed way problem?
Angular built-in have a way that your Angular app to support Internationalization. Still, the approach doesn't fit PWA apps because after you apply this approach, you don't have a single app, but in practice, you have an app for every language, so this is not compatible with PWA ecosystems. To find more detail, please check the [Github issue](https://github.com/angular/angular/issues/43796) and [StackOverflow question](https://stackoverflow.com/questions/61532813/how-to-enable-installation-of-the-multi-language-angular-pwa-with-single-service) that describe the problem.

Now I think we are on the same page. let's start.
## Use `ngx-translate`
Instead of using the built-in translation features of Angular, you can use ngx-translate.
The `ngx-translate` produce a single app at the end, so it fixes the built-in angular problem, as I mentioned before.

## a simple example
To demonstrate the solution I proposed, I prepared an example. You can see the code on [Github](https://github.com/behroozbc/pwa-translate-dome) or test the demo on [this link](https://behroozbc.github.io/pwa-translate-dome/). If you want more detail about `ngx-translate` see the `ngx-translate` [documentation](https://github.com/ngx-translate/core).

### The end

My goal is to help you! If you are still unsure or have questions about it, or if there are errors, please use the comments section below and let me know!