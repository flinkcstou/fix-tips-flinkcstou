 **source-map-explorer**

 - `npm intall -g source-map-explorer ` 

 - make symbol-link copy to bin-folder from node folder

- _IONIC_

- for ionic command is - `ionic build --source-map`

- `source-map-explorer www/build/main.js ./.sourcemap/main.js.map --html > result.html`
- `source-map-explorer www/build/main.js ./.sourcemap/main.js.map --json > result.json`


- _ANGULAR_ 

- for angular command is  создает в папке dist все файлы которые нужны source map и main.js 

- `source-map-explorer www/dis/main.js www/dist/main.js.map --html > result.html`

      official page - https://github.com/danvk/source-map-explorer


 **webpack-bundle-analyzer**
 
 нужно изучить
 
 
 **LogRocket**
 
 create new project in blog.logrocket.com 
 
 `npm i --save logrocket `
 
 add in app.component.ts
 
 example: 
 
          import LogRocket from 'logrocket';
          LogRocket.init('uo8yuw/aix-mobile');
          
          @Component({
            selector: 'app-root',
            templateUrl: 'app.component.html',
            styleUrls: ['app.component.scss']
          }) 


**caniuse-lite**
  
  изучить
  
  
