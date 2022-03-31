# Theory Summary
## A. Component Interaction (Parent to Child Communication)
### 1. @Input()
- In child component
- Receive values from parent component
Ex: 
` @Input() item = '';` <br/>
`<app-item-detail [item]="currentItem"></app-item-detail>` <br/>
_item_ : **target**, property in child component
_currentItem_ : property from parent component

**!**: watch @Input() property changes through OnChanges

### 2. @Output()
- In child component, tranfer data from child to parent	
- Using EventEmmit
Ex:
`@Output() newItemEvent = new EventEmitter<string>();` <br/>
`<app-item-output (newItemEvent)="addItem($event)"></app-item-output>` <br/>
_newItemEvent_: event in child component
_addItem()_: **target**, method in parent component

### 3. @ViewChild/@ViewChildren
- Provide access to child components
#### ViewChild decorator:
`@ViewChild(selector {read: readValue, static: staticValue}) property;`
-Kinds of `selector`: 
	+ Classes with `@Component` or `@Directive`
	+ Template reference: `<menu-item #aboutUs></menu-item>` 
	+ Provider defined in child componnent
	+ Using `TemplateRef`: the way to reference the `ng-template` in the component.
#### ViewChildren decorator:
- Configure a query list of child elements


## B. Pipe - Transform Data
- Using `@Pipe`
- implements PipeTransform
- have method transform()
- Can transform: date, uppercase, lowercase, currency, decimal, percent

## C. Component Store
- Manage component state, or based on "Service with a Subject"

