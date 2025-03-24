## Structure
```
rick-morty-challenge  
├── src  
├── dist
├── node_modules
├── public
├── src
    └── assets
    └── components
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

* ```CharacterTable.vue```: Create a table (extend also Bootstrap via package manager).
* ```App.vue```: Extend ```CharacterTable.vue``` to view.

Run the following command to install `Vite`.
```
npm install
```

You need decide an option to start the `Vite`.
```
# Compile and Hot-Reload for Development
npm run dev
```

```
# Compile and Minify for Production
npm run build
```