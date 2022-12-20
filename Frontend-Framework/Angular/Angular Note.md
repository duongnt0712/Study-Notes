# ANGULAR
## 1. Basic syntax
- `npm install -g @angular/cli`: install angular into project
- `ng new pj_name`: create new project
- `cd pj_name`: move inside project
- `ng serve -o`: run project and automatically open in localhost
<br/>
- `ng g c component_name`: create new component
- `ng g s service_name`: create new service
- `ng g class class_name`: create new model class

## 2. Introduction
**Angular** and **AngularJS** is completely **DIFFERENT**!
- Run in port 4200


## 3. String Interpolation
Within curly brace: `{{variable_here}}`
- Can execute expression, method 
- Cannot resolves 
	+ assignment (`=`, `+=`, `-=`)
	+ new, typeof, instanceof
	+ chaining expression (`++`, `--`)

**NOTE**: 
- Keep application logic in the componnent as much as possible!
- Expressions should finish quickly
- Template expression should not change any application state

## 4. How it works
### Flow
**Module**: inside `app.module.ts` file, can divide into multi module in purposes
includes
**Service** 
contains
**Component**

## 5. Component
Should divide into small components
- NavBar Component
- Sidebar Component
- Content Component
<br/> **Name file format**:
`<component_name>.<schematics>.ts`
Ex: app.component.ts

<br/> **Selector format**:
- Default: <app-component_name>
- Custom: in file `angular.json`
 
## 6. Data Binding
### Property Binding (Interpolation)
- Using Curly Brace for displaying text or string: 
`{{ variable_name }}`
<br/> Ex: {{ user.name }}
- Using SquareBrackets inside tag for binding data: 
`[textContent]="variable_name"`, `[src]="variable_name"`
<br/> Ex: `<input [type]="text" [value]="user.name">`

### Event Binding
Using `(event_name)="methodEventName()"`
<br/>Ex: `<button (click)="handler()"></button>`

### Two way DataBinding
Using FormsModule syntax (Part 9)

## 7. Life-cycle Hooks
7 types:
- OnInit
- OnChanges
- OnDestroy
- AfterViewInit
- AfterContentInit
- AfterViewChecked
- AfterContentChecked

## 8. Communication
### Input/Output
- `@Input() `Get the change from parents 
- `@Output() `Change the child without affect parent
### Service
Inside service.ts, use:
```
@Injectable({
	providedIn: 'root'
})
```
to apply this service to all component

### RxJS

## 9. Modules
### FormsModule
<br/> Ex: `[(ngModel)]="user.name"`

## 10. Structureal Directive
Adjust DOM structure
<br/> Syntax: `*ngIf`, `*ngFor`
### NgIf
- Using `<ng-template></ng-template>`
- `[Hidden]`: Prevent destroying the component.

### NgForOf
- index
- count
- first
- last
- even
- odd

## 11. Attribute Directive
### Class Binding
- `[class.class-name]`
- `[class]="array"`
- `[class]="object" {'class-name' : value }`
- `[class]="variable"`

### Style Binding
- `[style.tenStyle]`
- `[style.ten-style]`
- `[style.tenStyle.unit]`
- `[style]="object"`
- `[style.css-variable]`

## 12. Coding Convention
Using `trackBy` in `*ngFor`
`trackBy` can update the change of element without refresh all others which not tend to change.