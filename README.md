# Laravel Vue Tailwind Template

> __This is a template repo__

This repo is meant to serve as a template for Laravel projects that I want to use Vue and TailwindCSS on. This repo uses the following:

- __Laravel 7.*__
- __TailwindCSS 1.2.*__
- __Vue.js 2.6.*__
- __User Authentication:__ Uses the built in Laravel authentication system
- __BrowserSync:__ Automatic browser refreshing on file save
- __Laravel-Mix-Tailwind:__ Jeffrey Way plugin to simplify Laravel Mix config for TailwindCSS
- __Laravel-Mix-PurgeCSS__ Spatie plugin to simplify Laravel Mix config for PurgeCSS

It does __NOT__ use the official [Laravel Tailwindcss Frontend Preset](https://github.com/laravel-frontend-presets/tailwindcss) as it doesn't support v7 (yet).

### To Use

The following directions assume you are using Laravel Valet for local development. If not, you are on your own.

1. Click the 'Use This Template' button - Next to the 'Clone or Download' button above the file list of the repo

2. Fill in the fields on the resulting form and click create

3. Once created, clone the new repo. You will need to click the 'Clone or Download' button and copy the URL provided.

```shell
cd Your-Sites-Folder
git clone https://github.com/iAmBentley/aos.git new-project-name
cd new-project-name
```

4. Install Composer Dependencies

```shell
composer install
```

5. Install NPM Dependencies

This is technically two commands. 'Install' installs the dependencies and 'Run' compiles the css and javascript
 
```shell
npm install && npm run dev
```

6. Create a database

```shell
mysql -uroot -p
**** (enter your mysql password)
create database new-db-name;
show databases; // to confirm it was created
exit;
```

7. Create and Modify a .Env File

Technically not creating the file, but rather coping and modifiy it.

```shell
cp .env.example .env
code .env (code is a bash alias I use to open files in VS Code)
```

In VS Code, change the APP_NAME, APP_URL, DB_DATABASE, DB_USERNAME + DB_PASSWORD to the credentials used when making the database in step 6.

8. Run Initial Database Migrations

```shell
php artisan migrate
```

9. App Encryption Key

```shell
php artisan key:generate
```

10. [Optional] Serve the dev site locally over HTTPS

```shell
valet secure new-project-name
**** (enter computer users password)
```

__WARNING:__ After running Valet Secure, your site will no longer work. To fix this, replace the contents of your `webpack.mix.js` file with the following:

```javascript
const mix = require('laravel-mix');

// Required for BrowserSync to work with Valet Secure
const domain = 'lvt-template.test'; // <- Replace with your projects local domain
const homedir = require('os').homedir();

require('laravel-mix-tailwind');
require('laravel-mix-purgecss');

mix
    .js('resources/js/app.js', 'public/js')
    .postCss('resources/css/app.css', 'public/css')
	.tailwind('./tailwind.config.js')
	.browserSync({
		proxy: 'https://' + domain,
		host: domain,
		open: 'external',
		https: {
			key: homedir + '/.config/valet/Certificates/' + domain + '.key',
			cert: homedir + '/.config/valet/Certificates/' + domain + '.crt',
		}
	 });

if (mix.inProduction()) {
	mix
		.version()
		.purgeCss();
}
```

11. View the site in a browser

Visit new-project-name.test in your browser of choice. 


### Conclusion

You should be rocking and rolling at this point. If you see any problems or have suggestions to improve this template repo, please let me know by submitting an Issue or Pull Request on the repo.