## Code review Guidelines for angular & typescript
- Do not use timeout to delay navigation or hide any component. 
- Avoid using iFrames as it might create security concern.
- Do not add any component / Ui related code inside service. 
- Do not use `“any”`. Always use valid types
    ```yaml
    export class MyClass implements OnInit{
    ---
    meta: any; <====== Do not use "any"
    ---
    }
    ```
- Do not hardcode text in templates. Move all text to lang files and use language keys and language pipe
    - Avoid using string concatination use lang keys
    ```yaml
    <div>
    Contact Address <===== do not use hardcode txt
    ---
    {{'profile.ADDRESS_CONTACT_INFO' | lang }} <====== Use keys and langulage pipe
    </div>
    ```
 - Do not hardcode text in typescript/javascript files. Use lang file like above example
    ```yaml
    try{
    
    } catch(errorObj)
    {
    this.toaster.toast({ message: 'Failed to save data', <======Do not use 
    //somecode
    }
    ---
    try{
    
    } catch(errorObj)
    {
    this.toaster.toast({ message: this.languageService.get('profile.SAVE_ALERT'), <======mode all text to lang file
    //somecode
    }   
    ```
 - Use Css/SCSS class do not add/hardcode styles in Html
    ```yaml
    <div style="padding: 10px"> <===== do not use hardcode css
    ---
    <div class="ClassforStyle"> <===== use class present in file.
    ```

 - Do not use `&nbsp;&nbsp;&nbsp;`. Use css padding/margin as needed.
    - Do not us `<br/>` for new line. Use style to add line space. 
    ```yaml
    <div> 
    &nbsp;&nbsp;&nbsp;I am a Mentor   <===== do not use hardcode &nbsp;
    <br/>                              <=======do not write <BR/>
    I am Writing bad code 
    </div>
    ---
    <div> <===== use class present in file.
    <span class="PaddinLeft3">I am a Mentor</span>
    <spanclass="classOfBreakline">I am Writing Good & standard code </span>  
    </div>
    ```
- Use proper selector name for components w.r.t. to feature in project in place of generic selector
    - It's best practic to create components responsive.
    - Create component with single responsiblity
    ```yaml
    @Component({
    selector: 'app-demoselector'   <====== Selector name should not be generic it should be specific
    //somecode
    ---
    @Component({
    selector: 'employee-profile-demoselector'
    //somecode
    ```
- Use Project defined SASS variables for color & padding etc. DO not use hardcode css value.
    - Do not add hardcoded width on template or Css. use Bootstrap classes.
    ```yaml
    .MyClassForDiv{
    background-color: #000000;
    }
    ---
    .MyClassForDiv{
    background-color: $accent-1-dark;
    }
    ```
- Unsubscribe on ngOnDestroy if you have subscribed any object in component.
    ```yaml
    ngOninit():void{
    this.myObject= this.myObservable.Subscribe({
    //somecode
    }
    ngOnDestroy(){
    this.myObject.unsubscribe();  <===== Use Unsubscribe of every subscription.
    }    
    ```
- Do not push empty files 
- Services are singleton and class variables will get shared between components. 
    - Avoid having class variables inside service unless you are using as shared variables between different component instances. 
    - Reason : Angular creates only one instance of services by default.
    ```yaml
    @Injectabl()
    export class LearningMyService {
    provate notification: Notifications[];    <====== notifications will be shared between components. 
    }
    //some code    
    ```
 - Avoid calling Direct functions inside template as they get called in every change detection.Use functions only to events. 
    ```yaml
    <success-button [disabled]="IsDisabledFunction()"     <===== avoid calling this kind of function. Use variables 
                    (click)="ShowFunction()"              <====== Good to use
                    *ngIf="showVariable"                  <====== example of use class variables inplace of function
    ```
 - Avoid overriding library defined component styles
    ```yaml
    :: ng-deep my-list-view {                       <======= Avoid overriding 
    //some code
    }
    ```  
 - No need to use cathError if you are not doing anying with it. Error will be thrown autometically. 
    ```yaml
    Save(){
    //some code 
    .catch((errorObj)) => throw errorObj;               <====== Avoid catching and rethrowing 
    }
    ```  
 - Import lodash functions and use it in every component. Do not use Global
    ```yaml
    import {get, isEmpty, size} from 'lodash';
    ```
 
