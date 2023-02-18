# vue-scss-template
This is a template based on vite.js, vue.js, scss

# Installation
Clone the repo `git clone https://github.com/danieleln/vue-scss-template.git`, then
```
cd vue-scss-template
npm install
npm run dev
```

# File structure
```
.
├── README.md
├── index.html
├── package.json
└── src
    ├── assets
    │   ├── fonts
    │   └── images
    ├── js
    │   └── main.js
    ├── scss
    │   ├── abstracts
    │   │   ├── _functions.scss
    │   │   └── _mixins.scss
    │   ├── abstracts.scss
    │   ├── base
    │   │   ├── _reset.scss
    │   │   └── _themes.scss
    │   ├── classes
    │   │   └── _classes.scss
    │   ├── config
    │   │   ├── _globals.scss
    │   │   └── _variables.scss
    │   └── main.scss
    └── vue
        ├── App.vue
        ├── components
        └── pages
```

- `src`
    - the `assets` folder contains all the additional files, like fonts and images (inside the respective folders)
    - the `scss` folder contains all the `.scss` files
        - the `abstracts` folder contains functions & mixins that do not generate any output CSS code by themeselves
        - the `config` contains all the configuration files
            - `_globals.scss` is the main configuration file. It contains font-face definitions, colors and global parameters (like main font size, weight, ecc.)
            - `_variables.scss` contains the definition of some additional variables, like font sizes/weights, padding/margin sizes ecc...
        - the `base` folder contains default styling rules
            - `_reset.scss` contains some boilerplate code that resets default web browser styles
            - `_themes.scss` contains theme definitions.
        - `main.scss` links to the files that are inside the `base` and the `classes` folders. It should be included only in the `index.html` file.
        - `abstracts.scss` links to the `abstract` folder. It can be included in every vue component
    


## Documentation
### Importing fonts
to add font faces to scss do the following:
1. create the font folder inside `src/assets/fonts (eg. `src/fonts/My Font/`).
2. add files inside the folder you just created:
    ```
    .
    └── src
        └── assets
            └── fonts
                └── My Font
                    ├── MyFont-Italic-Light.ttf
                    ├── MyFont-Regular.ttf
                    └── MyFont-Bold.woff
    ```
3. edit `src/scss/config/_globals.scss` to acknowloedge scss that fonts has been added. You should edit the following map:
    ```
    $font-faces: [
        (
            family: "My Font",                              # font-family property
            folder: "MyFont",                               # name of the folder fonts/MyFont
            files: [
                (
                    style: italic,                          # font-style property
                    weight: 300,                            # font-weight property
                    format: truetype,                       # file format (truetype/eot/woff/woff2/svg)
                    filename: "MyFont-Italic-Light.ttf"     # file inside fonts/MyFont
                ),
                (
                    style: normal,
                    weight: 400,
                    format: truetype,
                    filename: "MyFont-Regular.ttf"
                ),
                (
                    style: normal,
                    weight: 700,
                    format: woff,
                    filename: "MyFont-Bold.woff"
                ),
            ]
        ),
    ];
    ```

### Colors definition
Colors are defined within the `src/scss/config/_globals.scss` file:
```
$colors: (
    dark: (
        400: #000,
    ),
    light: (
        400: #fff,
    ),
    accent: (
        400: #999,
    )
);
```
where 400 indicates the shade of the color. You can add different shades:
```
$colors: (
    accent: (
        300: #888,
        400: #999,
        500: #aaa,
    )
);
```
You can also add other color categories:
```
$colors: (
    dark: ( ... ),
    light: ( ... ),
    accent: ( ... ),
    primary: ( ... ),
    secondary: ( ... ),
);
```
scss automatically converts the map into css variables:
```
:root {
    --color-dark-400: #000;
    --color-light-400: #fff;
    --color-accent-300: #888;
    --color-accent-400: #999;
    --color-accent-500: #aaa;
    ...
}
```
NB: built-in light/dark themes depend on `--color-dark-400` and `--color-light-400`, so be cautios when editing those values!



### Adding themes
1. edit `src/scss/base/_themes.scss` and add a class with the colors of your choice:
    ```
    .my-new-cool-theme {
        --color-bg: ... ;
        --color-fg: ... ;
    }
    ```
    you should define at least those two properties.
    
