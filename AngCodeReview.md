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
