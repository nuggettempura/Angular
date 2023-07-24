# Angular
Parent to Child and Child to Parent Guide

*Angular uses TypeScript and it is a SPA (Single Page Application) where it renders only the components, not the entire application (Ex: Facebook).
*Different versions of Angular may vary!!!

component.ts file acts as a logic
component.html file acts as the interface

1. Data binding in component itself
- Use double curly brackets in the HTML from the typescript file to the HTML file

example: 

post.component.html  -----------> post.component.ts

<h1>{{ title }}</h1>              title: string = 'List of Posts';

2. Data binding between parent to child

Passing from parent -> child needs a a built in lifecycle hook in Angular called "AfterViewInit/ngAfterViewInit". This will initialize the component right after it is called after the constructor of the component is set up.

- @Input() decorator to give access for the child to get the data from the parent.

	app.component.ts                ---->                    app.component.html                    ---->       post.component.ts           ---->           post.component.html
- parentMessage: string = 'Message';            <app-post [fromParent]="parentMessage"></app-post>              @Input() fromParent = '';                  <h3>{{ fromParent }}</h3> 

- [fromParent] and "parentMessage" can have any name. give it a name


-- See example app.component.ts & app.component.html -> post.component.ts & post.component.html

App component (parent)  -> navbar component (child component)
			-> post component



3. Data binding between child to parent

@ViewChild() decorator

Event Emitter & @Output() decorator - Ideal if we want to share data that occur on things like button clicks, form entries, and other user events.

* The example will be made through a click button that will render in the HTML

a. Declare @Output with a name at a child component ex: @Output() messageEvent = new EventEmitter<string>();
b. Then, declare in the HTML file a button: <button (click)="sendMessage()">Click</button>. Angular uses (click) for click events.
c. Next, declare what message we want to pass in the ts file : outputChildMessage: string = 'Message from Child Component Via Output';
d. Put the function and use "emit" to call out the message : this.messageEvent.emit(this.outputChildMessage)
e. Pass the messageEvent data to the parent HTML : (messageEvent)="receiveMessage($event)" 
f. Declare a function in the ts file for the parent file to receive the message : receiveMessage($event: string) {
    this.fromChildOutput = $event;
  }
   Along with a property of fromChildOutput to call out in the function
g. Pass it back to the HTML : <p>{{ fromChildOutput }}</p>

*Sorry if it is a bit lengthy, 





