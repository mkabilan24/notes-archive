AngularNodejs

!Part 1: Steps!

1) Open Command Terminal (cmd)
2) Check Node Version -> node -v
3) View files/folders in directory -> dir
4) Enter Directory(Folder) -> cd {folder name}
5) Create Angular Folder -> mkdir Angular
6) Enter Angular Directory -> cd Angular
6) Create typescript Folder -> mkdir typescript
7) Enter typescript Directory -> cd typescript
8) Check Node Package Manager(npm) Version -> npm -v
9) Initialize Node Package Manager -> npm init

	C:\Users\2957076\Desktop\Angular\typescript>npm init
	This utility will walk you through creating a package.json file.
	It only covers the most common items, and tries to guess sensible defaults.

	See `npm help init` for definitive documentation on these fields
	and exactly what they do.

	Use `npm install <pkg>` afterwards to install a package and
	save it as a dependency in the package.json file.

	Press ^C at any time to quit.
	package name: (typescript) typescript-demo
	version: (1.0.0)
	description: A sample application to learn typescript
	entry point: (index.js)
	test command:
	git repository:
	keywords:
	author: 2957076
	license: (ISC)
	type: (commonjs)
	About to write to C:\Users\2957076\Desktop\Angular\typescript\package.json:

	{
  	"name": "typescript-demo",
  	"version": "1.0.0",
  	"description": "A sample application to learn typescript",
  	"main": "index.js",
  	"scripts": {
    	"test": "echo \"Error: no test specified\" && exit 1"
  	},
  	"author": "2957076",
  	"license": "ISC",
  	"type": "commonjs"
	}


	Is this OK? (yes)

10) Enter package.json through VSCode -> code .

!Part 2: Steps!

11) Open Windows Powershell
12) View files/folders in directory -> ls
13) Enter Angular Directory ->  cd .\Angular\
14) Create Application using Node Package Execute (npx) -> npx @angular/cli@15.2.7 new sample-application

	Need to install the following packages:
	@angular/cli@15.2.7
	Ok to proceed? (y) y

	npm warn deprecated inflight@1.0.6: This module is not supported, and leaks memory. Do not use it. Check out lru-cache if 	you want a good and tested way to coalesce async requests by a key value, which is much more comprehensive and powerful.
	npm warn deprecated @npmcli/move-file@2.0.1: This functionality has been moved to @npmcli/fs
	npm warn deprecated npmlog@6.0.2: This package is no longer supported.
	npm warn deprecated are-we-there-yet@3.0.1: This package is no longer supported.
	npm warn deprecated read-package-json@6.0.4: This package is no longer supported. Please use @npmcli/package-json instead.
	npm warn deprecated rimraf@3.0.2: Rimraf versions prior to v4 are no longer supported
	npm warn deprecated glob@7.2.3: Glob versions prior to v9 are no longer supported
	npm warn deprecated glob@8.1.0: Glob versions prior to v9 are no longer supported
	npm warn deprecated gauge@4.0.4: This package is no longer supported.
	npm warn deprecated glob@7.2.3: Glob versions prior to v9 are no longer supported
	? Would you like to share pseudonymous usage data about this project with the Angular Team
	at Google under Google's Privacy Policy at https://policies.google.com/privacy. For more
	details and how to change this setting, see https://angular.io/analytics. No
	Global setting: disabled
	Local setting: No local workspace configuration file.
	Effective status: disabled
	? Would you like to add Angular routing? Yes
	? Which stylesheet format would you like to use? CSS
	CREATE sample-application/angular.json (2760 bytes)
	CREATE sample-application/package.json (1049 bytes)
	CREATE sample-application/README.md (1071 bytes)
	CREATE sample-application/tsconfig.json (901 bytes)
	CREATE sample-application/.editorconfig (274 bytes)
	CREATE sample-application/.gitignore (548 bytes)
	CREATE sample-application/tsconfig.app.json (263 bytes)
	CREATE sample-application/tsconfig.spec.json (273 bytes)
	CREATE sample-application/.vscode/extensions.json (130 bytes)
	CREATE sample-application/.vscode/launch.json (470 bytes)
	CREATE sample-application/.vscode/tasks.json (938 bytes)
	CREATE sample-application/src/favicon.ico (948 bytes)
	CREATE sample-application/src/index.html (303 bytes)
	CREATE sample-application/src/main.ts (214 bytes)
	CREATE sample-application/src/styles.css (80 bytes)
	CREATE sample-application/src/assets/.gitkeep (0 bytes)
	CREATE sample-application/src/app/app-routing.module.ts (245 bytes)
	CREATE sample-application/src/app/app.module.ts (393 bytes)
	CREATE sample-application/src/app/app.component.html (23115 bytes)
	CREATE sample-application/src/app/app.component.spec.ts (1109 bytes)
	CREATE sample-application/src/app/app.component.ts (222 bytes)
	CREATE sample-application/src/app/app.component.css (0 bytes)
	✔ Packages installed successfully.
	'git' is not recognized as an internal or external command,
	operable program or batch file.

15) Enter Application -> cd .\sample-application\
16) Enter Application through VSCode -> code .
17) Start Application -> npm run start              
18) Generate new Component -> npm run ng generate component
19) Generate new Service -> npm run ng g s service