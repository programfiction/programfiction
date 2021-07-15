## Code review Guidelines for angular & typescript

-	Do not use `“any”`. Always use valid types
    ```yaml
    export class MyClass implements OnInit{
    ---
    meta: any; <====== Do not use "any"
    ---
    }
    ```
- Do not hardcode text in templates. Move all text to lang files and use language keys and language pipe
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
    ```yaml
    @Component({
    selector: 'app-demoselector'   <====== Selector name should not be generic it should be specific
    //somecode
    ---
    @Component({
    selector: 'employee-profile-demoselector'
    //somecode
    ```
- Use Project defined SASS variabs for color & padding etc. DO not use hardcode css value.
    ```yaml
    .MyClassForDiv{
    background-color: #000000;
    }
    ---
    .MyClassForDiv{
    background-color: $accent-1-dark;
    }
    ```
