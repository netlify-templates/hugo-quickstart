 [![hugo + netlify](https://res.cloudinary.com/dzkoxrsdj/image/upload/v1656562989/template_1_edyp8b.png)](https://ntl.fyi/3P9w1mr)

# Hugo Quickstart Template   

This is a bare-bones Hugo project that has everything you need to quickly deploy it to [Netlify](https://netlify.com). 

Hate reading, here's a video: https://youtu.be/t-tsRxxYdpk

Love reading, here's blog post: https://www.netlify.com/blog/deploy-your-hugo-app-quick/

## Table of Contents:

- [Quick Setup + Deploy Option](#quick-setup--deploy-option)
- [Regular Setup](#regular-setup)
  - [Cloning + Install Packages](#1-cloning--install-packages)
  - [Deploying](#2-deploying)
- [Styling](#styling)
  - [Notes on Styling](#notes-on-styling)
  - [Remove Styling](#remove-styling)
- [Hugo + Netlify Resources](#hugo--netlify-resources)
- [Testing](#testing)
  - [Included Default Testing](#included-default-testing)
  - [Removing Renovate](#removing-renovate)
  - [Removing Cypress](#removing-cypress)
- [Want to learn more?](#want-to-learn-more)

## Quick Setup + Deploy Option

Click this button and it will help you create a new repo, create a new Netlify project, and deploy!

[![Deploy to Netlify Button](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/netlify-templates/hugo-quickstart)

## Regular Setup

 ### 1. Cloning + Running Locally

  - Clone this repo with one of these options:

    - Click the 'Use this template' button at the top of the page
    - Or via the command line `git clone https://github.com/netlify-templates/hugo-quickstart`

 - Start the Hugo sever & check it out:

   - `hugo server -D`
   - go to [http://localhost:1313/](http://localhost:1313/)

  > Alternatively, you can run this locally with [the Netlify CLI](https://docs.netlify.com/cli/get-started/)'s by running the `netlify dev` command for more options like receiving a live preview to share (`netlify dev --live`) and the ability to test [Netlify Functions](https://www.netlify.com/products/functions) and [redirects](https://docs.netlify.com/routing/redirects/). 

  ### 2. Deploying
  - Install the Netlify CLI globally `npm install netlify-cli -g`
    
  - Run `hugo`

  - Then use the `netlify deploy` for a deploy preview link or `netlify deploy --prod` to deploy to production

  Here are a few other ways you can deploy this template:
    
  - Use the Netlify CLI's create from template command `netlify sites:create-template hugo-quickstart` which will create a repo, Netlify project, and deploy it
    
  - If you want to utilize continuous deployment through GitHub webhooks, run the Netlify command `netlify init` to create a new project based on your repo or `netlify link` to connect your repo to an existing project

## Styling

We've added some modern styling to this template using Sass within an external stylesheet, this will allow you to easily remove our styling and add in your own. 

If you decide that you want to keep our styling you can review our style notes below. 

### Notes on Styling

The [`demo-styling.scss`](https://github.com/netlify-templates/hugo-quickstart/blob/main/assets/sass/demo-styling.scss) is located within the assets folder in the root directory. Within the `head.html` file you will notice that there are Hugo pipes set up to transpile sass into css. `resources.Get` retreives the scss file within the asset directory as a resource and `resources.ToCSS` takes that resource and converts it into a css file that can be read. Within the link tag for the stylesheet we link to the new css file by using `$style.RelPermalink`

If you decide to keep using Sass within Hugo you will needs to keep the below snippet of code and update the file path of your stylesheet if needed. 

```html
  {{ $sass := resources.Get "/sass/demo-styling.scss" }}
  {{ $style := $sass | resources.ToCSS }}
  <link rel="stylesheet" href="{{ $style.RelPermalink }}">
```

The variables below give you the ability to change the gradient colors of the blobs and are interpolated into the URL string of the background-img within the body. 

```scss
// Controls the blob blur gradient colors within the body background image url
$top-right-blur-1: '20C6B7';
$top-right-blur-2: '4D9ABF';
$bttm-left-blur-1: 'FF5C02';
$bttm-left-blur-2: 'FFCDB1';

...

body{
    background-image: url("data:image/svg+xml,%3Csvg width='1728' height='1235' viewBox='0 0 1728 1235' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cg opacity='0.75' filter='url(%23filter0_f_39_143)'%3E%3Ccircle cy='1000' r='264' fill='url(%23paint0_linear_39_143)'/%3E%3C/g%3E%3Cg opacity='0.65' filter='url(%23filter1_f_39_143)'%3E%3Ccircle cx='1720' cy='264' r='379' fill='url(%23paint1_linear_39_143)'/%3E%3C/g%3E%3Cdefs%3E%3Cfilter id='filter0_f_39_143' x='-485' y='515' width='970' height='970' filterUnits='userSpaceOnUse' color-interpolation-filters='sRGB'%3E%3CfeFlood flood-opacity='0' result='BackgroundImageFix'/%3E%3CfeBlend mode='normal' in='SourceGraphic' in2='BackgroundImageFix' result='shape'/%3E%3CfeGaussianBlur stdDeviation='110.5' result='effect1_foregroundBlur_39_143'/%3E%3C/filter%3E%3Cfilter id='filter1_f_39_143' x='1120' y='-336' width='1200' height='1200' filterUnits='userSpaceOnUse' color-interpolation-filters='sRGB'%3E%3CfeFlood flood-opacity='0' result='BackgroundImageFix'/%3E%3CfeBlend mode='normal' in='SourceGraphic' in2='BackgroundImageFix' result='shape'/%3E%3CfeGaussianBlur stdDeviation='110.5' result='effect1_foregroundBlur_39_143'/%3E%3C/filter%3E%3ClinearGradient id='paint0_linear_39_143' x1='196.5' y1='902' x2='-2.55853e-05' y2='1264' gradientUnits='userSpaceOnUse'%3E%3Cstop stop-color='%23#{$bttm-left-blur-1}'/%3E%3Cstop offset='1' stop-color='%23#{$bttm-left-blur-2}'/%3E%3C/linearGradient%3E%3ClinearGradient id='paint1_linear_39_143' x1='1720' y1='-115' x2='1720' y2='643' gradientUnits='userSpaceOnUse'%3E%3Cstop stop-color='%23#{$top-right-blur-1}'/%3E%3Cstop offset='1' stop-color='%23#{$top-right-blur-2}'/%3E%3C/linearGradient%3E%3C/defs%3E%3C/svg%3E");
    ...
  }
```

## Remove Styling

If you decide that our styling is not for you, all you'll need to do is remove the [demo-styling.scss](https://github.com/netlify-templates/hugo-quickstart/blob/main/assets/sass/demo-styling.scss) file. 

## Hugo + Netlify Resources

Here are some resources to help you on your Hugo + Netlify coding fun!

- [Hugo on Netlify Integration Page](https://ntl.fyi/3P9w1mr)


Hope this template helps :) Happy coding 👩🏻‍💻!

---

## Testing

### Included Default Testing

We’ve included some tooling that helps us maintain these templates. This template currently uses:

- [Renovate](https://www.mend.io/free-developer-tools/renovate/) - to regularly update our dependencies
- [Cypress](https://www.cypress.io/) - to run tests against how the template runs in the browser
- [Cypress Netlify Build Plugin](https://github.com/cypress-io/netlify-plugin-cypress) - to run our tests during our build process

If your team is not interested in this tooling, you can remove them with ease!

### Removing Renovate

In order to keep our project up-to-date with dependencies we use a tool called [Renovate](https://github.com/marketplace/renovate). If you’re not interested in this tooling, delete the `renovate.json` file and commit that onto your main branch.

### Removing Cypress

For our testing, we use [Cypress](https://www.cypress.io/) for end-to-end testing. This makes sure that we can validate that our templates are rendering and displaying as we’d expect. By default, we have Cypress not generate deploy links if our tests don’t pass. If you’d like to keep Cypress and still generate the deploy links, go into your `netlify.toml` and delete the plugin configuration lines:

```diff
[[plugins]]
  package = "netlify-plugin-cypress"
-  [plugins.inputs.postBuild]
-    enable = true
-
-  [plugins.inputs]
-    enable = false 
```

If you’d like to remove the `netlify-plugin-cypress` build plugin entirely, you’d need to delete the entire block above instead. And then make sure sure to remove the package from the dependencies using:

```bash
npm uninstall -D netlify-plugin-cypress
```

And lastly if you’d like to remove Cypress entirely, delete the entire `cypress` folder and the `cypress.config.ts` file. Then remove the dependency using:

```bash
npm uninstall cypress
```
