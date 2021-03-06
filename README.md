# About this Fork

The purpose of this fork is to be able to use ng2-material-select with **angular-cli-beta.22-1**

When you upgrade to that version of angular-cli, you will see this error:
> Error: Ng2SelectModule is not an NgModule

I'm not that familiar with webpack and didn't want to spend time migrating ng2-material-select's webpack config from version 1 to 2. So instead, I just decided to compile the source code directly as part of the angular-cli project.

## Instructions

Note: If your angular-cli project isn't setup for SCSS, I don't think this will work.

Add these dependencies to **package.json**
```json
    "equals": "^1.0.5",
    "ng2-material-dropdown": "arlowhite/ng2-material-dropdown",
    "ng2-material-select": "arlowhite/ng2-material-select",
```

`npm install`

Create *src/equals.d.ts*
```ts
declare var equal:EqualStatic;

declare module 'equals' {
  export = equal;
}

type EqualStatic = (a: any, b: any, memos?: any) => boolean;
```

That should be it. Try `ng serve`


# Angular2 Material Select

A component inspired by material design for creating visually nice select components.

**This is still WIP**

## Demo
Checkout a live demo at [http://www.webpackbin.com/4kAEf9Sub](http://www.webpackbin.com/4kAEf9Sub)

## Install

    npm install ng2-material-select --save

## API
- `placeholder` - defines the placeholder when no items are selected
- `multiple` - defines whether it's possible to select multiple items


#### Example
```html
<ng2-select [placeholder]="'Choose your framework'"
            [options]="options"
            [(ngModel)]="framework">

</ng2-select>
```
```javascript
// import module
import { Ng2SelectModule } from 'ng2-material-select';

@NgModule({
    imports: [ Ng2SelectModule ]
    // ..
})
export class MyModule {}
```

## Advanced Usage using objects

In case you want to use objects instead of simple arrays, you might want to use 3 further options:
- **`displayBy`** - defines the key for displaying the value of the item

- **`?selectedDisplayBy`** - optional, defines the key for displaying the value once an item is selected

- **`?identifyBy`** - optional, it is useful in case there is the possibility to have items with duplicate values (ex. two items with the same name). In that case, you can defined another key (ex. id) to correctly identify the item. Also, this allows the component to use `trackBy`

In addition to that you may listen to a change event to get notified whenever a new option has been selected:

- **onChange** - optional, fires whenever a new option gets selected

#### Example
```html
<ng2-select [placeholder]="'Choose your framework'"
            [displayBy]="'name'"
            [selectedDisplayBy]="'label'"
            [identifyBy]="'name'"
            [options]="options"
            [(ngModel)]="framework">
</ng2-select>
```
```javascript
import { Component } from '@angular/core';

@Component({
    selector: 'app',
    template: require('./home.html')
})

export class App {
    framework = 'Angular 2';
    options = [
        {
            name: 'Angular2',
            label: 'ng2',
            id: 0
        },
        {
            name: 'React',
            label: 'rx',
            id: 1
        }
    ];
}
 ```   

## TODO
- Autocomplete dropdown
- Nicer design
