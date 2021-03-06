# Ionic Scroll Hide

This plugin was inspired by [Ionic Scroll Sista](https://github.com/djett41/ionic-scroll-sista). Tested in Ionic 2 and 3.

## Setup

1. Install jQuery library
```
npm install --save jquery
```
2. Copy `scroll-hide` folder into your Ionic project (src/components).
3. When using Ionic 2, remember to uncomment the line 547 and comment the line 545 (inside the `onContentScroll()` of `ScrollHide`).
```typescript
export class ScrollHide implements OnInit, OnDestroy {
	...
	onContentScroll(event: ScrollEvent, isMoveEnd: boolean) {

		// For Ionic 3
		//let maxScrollTop = this.content._scrollContent.nativeElement.scrollHeight - (event.contentTop + event.contentHeight + event.contentBottom) - (this.extendBottom ? this.footerHeight : 0);
		// For Ionic 2
		let maxScrollTop = this.content._scrollEle.scrollHeight - (event.contentTop + event.contentHeight + event.contentBottom) - (this.extendBottom ? this.footerHeight : 0); // For ionic2
		...
	}
	...
}
```
4. Add `ScrollHide` class to the declarations NgModule metadata.
#### app.module.ts
```typescript
import { ScrollHide } from './../components/scroll-hide/scroll-hide';

@NgModule({
    declarations: [
        MyApp,
        ...
        ScrollHide,
    ],
    ...
})
export class AppModule { }
```

## Usage

Scroll Hide is an attribute directive, and requires an input of `viewCtrl`. So, rememeber to inject ViewController into the page constrcutor. To enable the plugin, add `[scroll-hide]="viewCtrl"` into `ion-content`.


There are three transistion types can be used for each `ion-toolbar`, they are `Static`, `Translate`, `Shrink`.

#### Static
The toolbar would not be translated and shrinked during scrolling. It is the default type.

![Static](readme/static.gif)

#### Translate
The toolbar would be translated during scrolling. To enable, add an attribute of `scroll-hide-translate` into ion-toolbar.

![Translate](readme/translate.gif)

#### Shrink
The toolbar would be shrinked during scrolling. To enable, add an attribute of `scroll-hide-shrink="shrinkVal"` into ion-toolbar, where `shrinkVal` is the maximum percentage of shrinking, defualt to 1.

|shrinkVal = 1						| shrinkVal = 0.5						|
------------------------------------|---------------------------------------|
|![Shrink 1](readme/shrink-1.gif)	| ![Shrink 0.5](readme/shrink-0.5.gif)	|


## Example

#### home.ts
```typescript
import { Component } from '@angular/core';
import { NavController, ViewController } from 'ionic-angular';

@Component({
    selector: 'page-home',
    templateUrl: 'home.html'
})
export class HomePage {

    constructor(public navCtrl: NavController, 
                public viewCtrl: ViewController) {}
}
```
#### home.html
```html
<ion-header>
    <ion-navbar color="primary">
        <ion-title>Home</ion-title>
    </ion-navbar>
    
    <ion-toolbar color="primary" scroll-hide-translate>
        <ion-searchbar></ion-searchbar>
    </ion-toolbar>
</ion-header>

<ion-content padding [scroll-hide]="viewCtrl">
    <h2>Welcome to Ionic!</h2>
</ion-content>
```