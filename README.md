## Structure
```
rick-morty-challenge  
├── src  
├── dist
├── node_modules
├── public
├── src
    ├── assets
    |   └── base.css
    |   └── logo.svg
    |   └── main.css
    ├── components
    |   └── icons
    |   └── CharacterTable.vue
    |   └── HelloWorld.vue
    |   └── TheWelcome.vue
    |   └── WelcomeItem.vue
    App.vue
├── index.html
├── package.json
├── README.md
├── vite.config.js   
```

* ```CharacterTable.vue```: Create a table (extend also ```Bootstrap``` via package manager).
* ```App.vue```: Extend ```CharacterTable.vue``` to view.

Run the following command to install `Vite`.
```
npm install
```

You need decide an option to start the `Vite`.
```
# Compile and hot-reload for development
npm run dev
```

```
# Compile and minify for production
npm run build
```

## Subject about deploy

Change ```vite.config.js``` and add ```base: '/rick-morty-challenge/,'``` to create a root repository to make redirectioning routes from project.

Also is necessary use ```Vite``` to get a good working, use ```build``` option.