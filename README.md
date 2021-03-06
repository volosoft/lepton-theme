This repo is to collect feedback and issues about LeptonX from the community, and share changelogs about the releases. 

## Open-Source

To add `LeptonX-lite` into your project,

* Install `@abp/ng.theme.lepton-x`

`npm install @abp/ng.theme.lepton-x@preview` or 

`yarn add @abp/ng.theme.lepton-x@preview`

* Then, we need to edit the styles array in `angular.json` to replace the existing style with the new one.

Add the following style 

```json
"node_modules/bootstrap-icons/font/bootstrap-icons.css",
```

* Finally, remove `ThemeBasicModule` from `app.module.ts` and `shared.module.ts`, and import the related modules in `app.module.ts`

```js
import { ThemeLeptonXModule } from '@abp/ng.theme.lepton-x';
import { SideMenuLayoutModule } from '@abp/ng.theme.lepton-x/layouts';

@NgModule({
  imports: [
    // ...

    // do not forget to remove ThemeBasicModule
    //  ThemeBasicModule.forRoot(),
    ThemeLeptonXModule.forRoot(),
    SideMenuLayoutModule.forRoot(),
  ],
  // ...
})
export class AppModule {}
```

Note: If you employ [Resource Owner Password Flow](https://docs.abp.io/en/abp/latest/UI/Angular/Authorization#resource-owner-password-flow) for authorization, you should import the following module as well:

```js
import { AccountLayoutModule } from '@abp/ng.theme.lepton-x/account';

@NgModule({
  // ...
  imports: [
    // ...
    AccountLayoutModule.forRoot(),
    // ...
  ],
  // ...
})
export class AppModule {}
```

To change the logos and brand color of the `LeptonX`, simply add the following CSS to the `styles.scss`

```css
:root {
  --lpx-logo: url('/assets/images/logo.png');
  --lpx-logo-icon: url('/assets/images/logo-icon.png');
  --lpx-brand: #edae53;
}
```

- `--lpx-logo` is used to place the logo in the menu.
- `--lpx-logo-icon` is a square icon used when the menu is collapsed. 
- `--lpx-brand` is a color used throughout the application, especially on active elements. 

## Commercial

To add `LeptonX` into your existing projects, 

* Firstly, install `@volosoft/abp.ng.theme.lepton-x`

`npm install @volosoft/abp.ng.theme.lepton-x@preview` or 

`yarn add @volosoft/abp.ng.theme.lepton-x@preview`

* Then, edit `angular.json` as follows:

Remove the following config from the `styles` array since LeptonX provides bootstrap as embedded in its CSS.

```JSON
{
  "input": "node_modules/bootstrap/dist/css/bootstrap.min.css",
  "inject": true,
  "bundleName": "bootstrap-ltr.min"
},
```

Add the following ones into the `styles` array

```JSON
"node_modules/bootstrap-icons/font/bootstrap-icons.css",
```

Three of them are related to the theming and will be loaded during runtime. That's why they are not injected into the `head` as a style. Hence, the `"inject": false`

The fourth one depends on which layout you want to use. For now, there is only `sidemenu-layout` available. In the future, there will be many layouts to choose from. 

The last one is `bootstrap-icons` which are being used throughout the components. 

* At last, remove `ThemeLeptonModule` from `app.module.ts` and `shared.module.ts`, and import the following modules in `app.module.ts`

```js
import { ThemeLeptonXModule } from '@volosoft/abp.ng.theme.lepton-x';
import { SideMenuLayoutModule } from '@volosoft/abp.ng.theme.lepton-x/layouts';

@NgModule({
  // ...
  imports: [
    // ...
    // ThemeLeptonModule.forRoot(),
    ThemeLeptonXModule.forRoot(),
    SideMenuLayoutModule.forRoot(), // depends on which layout you choose
    // ...
  ],
  // ...
})
export class AppModule {}
```

Note: If you employ [Resource Owner Password Flow](https://docs.abp.io/en/abp/latest/UI/Angular/Authorization#resource-owner-password-flow) for authorization, you should import the following module as well:

```js
import { AccountLayoutModule } from '@volosoft/abp.ng.theme.lepton-x/account';

@NgModule({
  // ...
  imports: [
    // ...
    AccountLayoutModule.forRoot({
      layout: {
        authLayoutImg: '/assets/images/login-bg.jpg',
      },
    }),
    // ...
  ],
  // ...
})
export class AppModule {}
```

`authLayoutImg`: (Optional) If not given, a default image will be placed on the authentication pages.


* At this point, `LeptonX` theme should be up and running within your application. However, you may need to overwrite some css variables based your needs for every theme available as follows:
  
```scss
:root {
  .lpx-theme-dark {
    --lpx-logo: url('/assets/images/logo/logo-light.svg');
    --lpx-logo-icon: url('/assets/images/logo/logo-light-icon.svg');
    --lpx-brand: #edae53;
  }

  .lpx-theme-dim {
    --lpx-logo: url('/assets/images/logo/logo-light.svg');
    --lpx-logo-icon: url('/assets/images/logo/logo-light-icon.svg');
    --lpx-brand: #f15835;
  }

  .lpx-theme-light {
    --lpx-logo: url('/assets/images/logo/logo-dark.svg');
    --lpx-logo-icon: url('/assets/images/logo/logo-dark-icon.svg');
    --lpx-brand: #69aada;
  }
}
```
If everything is ok, you can remove the `@volo/abp.ng.theme.lepton` in package.json