# Symfony Vue Encore Docker Environment

### 1. create a Symfony Project named app with this command

```
symfony new app --version="6.3.*" --webapp
```


### 2. cd app/ & install Encore

```

composer require symfony/webpack-encore-bundle

yarn install

```

### 3. enable Vue in webpack.config.js

```
Encore

    .addEntry('app', './assets/app.js')

    .enableVueLoader()

```

### 4. install Vue.js

```

yarn add --dev vue vue-loader vue-template-compiler

```

### 5. create app.js in app/assets/js/ & mount app 
```js

import { createApp } from 'vue'
import App from './components/App';

const app = createApp(App)

app.mount('#app')

```

### 6. create assets/js/components folder & add your App.vue Component
```js

<template>
    <div id="app">
        Hi
    </div>
</template>

<script>
    export default {
        name: 'app'
    }
</script>

```

### 7. import app.js in app/assets/app.js

```js

/*
 * Welcome to your app's main JavaScript file!
 *
 * We recommend including the built version of this JavaScript file
 * (and its CSS file) in your base layout (base.html.twig).
 */

// any CSS you import will output into a single css file (app.css in this case)
import './styles/app.css';

import './js/app.js';

```

### 8. change .env variables for the database

```

SYMFONY_APP_PATH=./app

# mysql
MYSQL_ROOT_PASSWORD=root
MYSQL_DATABASE=new_docker_project_db
MYSQL_USER=root
MYSQL_PASSWORD=root

```

### 9. add base controller in symfony 

``` 

php bin/console make:contoller Base

```

```php

class BaseController extends AbstractController
{
    #[Route('/', name: 'app_base')]
    public function index(): Response
    {
        return $this->render('base.html.twig');
    }
}

```

### add #app to your base.html.twig file
```twig

<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>{% block title %}Welcome!{% endblock %}</title>
        
        {% block stylesheets %}
            {{ encore_entry_link_tags('app') }}
        {% endblock %}

        {% block javascripts %}
            {{ encore_entry_script_tags('app') }}
        {% endblock %}
    </head>
    <body>
        {% block body %}
            <div id="app"></div>
        {% endblock %}
    </body>
</html>

```

### at the end docker compose build & docker compose up to run the local environment 🍑