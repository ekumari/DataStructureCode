https://www.youtube.com/watch?v=W5dEbsHrb9k&t=1592s

Issues while creating web application using javascript

*   Boiler - Plate code: means writting repeative lines of code which are common across the application
*   Maintenance - JavaScript is unstructured hence,dificult to maintain unstructure application 
*   Change - difficult to implement changes
*   Compatibility - device or browser
*   Focus - focus on business logic

Angular helps you to solve above problem.

Angular is a framework which is used to create structure, dynamic web application resolving all the above issues and let's developer focus on the business logic.

Angular uses typescript as programming langauge

Framework provides you the basic template and implementing the best practises, design pattern that any developer should follow for creating structured application.

*   Angular is built on basic 2 concepts: -
    - SPA: Single Page Application e.g GMAIL single content page based on clicks, contents get changed.
    - Dependency Injection

Pre-requisite:
*   HTML
*   CSS
*   javascript

Good to know:
*   XML/JSON
*   HTTP Verbs
*   REST Services

### Folder Structure:

    - package.json: contains command which we want to use, dependencies that angular uses.
    - nodes_modules: contains downloaded dependencies
    - angular.json: configuration reqd to compile and execute angular project
        - index.html
        - main.ts : src/main.ts - main of the main entrypoint file
        - assest: images, videos
        - styles: provides styles style.css - css apply globally from this file
    - app.modules: import modules so that angular knows
        - bootstrap:[AppComponent]
        - configure all the angular app. level stuff

ng serve - Start your application and compiles all the typescript files and launch the app on localhost:4200
ng build - build your app

PlatformBrowserDynamic - handles all browser related compatibility issue


    - Component: provide binding of data with the view

### one-way data binding
*   String Interpolation: {{title}} 
*   [src] using square bracket

Event binding use (click)=show()
Data binding use [square bracket]

*ngFor
*ngIf