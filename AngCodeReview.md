Code review Guidelines for angular & typescript
-	Do not use `“any”`. Always use valid types
  ```yaml
  export class MyClass implements OnInit{
  ---
  meta: any; <====== Do not use "any"
  ---
  }
  ```
