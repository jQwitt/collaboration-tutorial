# Environment Configurations

Using create-react-app, we will be walking through a few of the configurations we will be adding to our environment to ensure the quality of the codebase.

We will be adding:

-   Prettier, our code formatter and style enforcer
-   ESLint, our linter and first defense against bugs
-   Git Hooks, lets us automatically double check correctness and format

# Prettier

Add the extension from the VSCode marketplace [LINK](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

Also run `yarn add -D prettier` to add it to the project as a dependency.

Next go to your VSCode settings (command , on Mac) and type 'Format' into the search bar. Ensure that the default formatter is set to `prettier-vscode` and 'Format On Save' is checked.

Here we can add a `.prettierrc` file to configure our style rules. I've added one already, so feel free to change some rules and get a feel for how it works!

Lastly, we can add a `.prettierignore` file to exclude parts of our code we don't want to format. Checkout the one in the project for more info.

To confirm its working, run `yarn prettier -c src` to check for errors, and `yarn prettier -w src` to overwrite them.

# ESLint

Add the extension from the VSCode marketplace [LINK](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

Also run `yarn add -D eslint` to add it to the project as a dependency.

To use existing standartization, we will just extend the AirBnb configurtion as done in this [article](https://blog.echobind.com/integrating-prettier-eslint-airbnb-style-guide-in-vscode-47f07b5d7d6a).

Here we can add a `.eslintrc` file to override or add to the AirBnb rules, as well as a `.eslintrcirngore` file to exclude parts of our code we don't want to lint.

To confirm its working, run `eslint src` to check for errors, and `yarn prettier -w src` to overwrite them.

# Git Hooks

Now that we have some basic formatting and linting, we want to automate them in order to ensure they run before code is pushed to the repository. We will be using a package called Husky to make our lives easier

Run the command `yarn add -D husky` to add the package as a dependency. We will also add a package `yarn add -D lint-staged` to work with Husky.

Finally, add this snippet to your `package.json`:

```json 
"husky": { 
    "hooks": { 
        "pre-commit": "lint-staged" 
    } 
 }, 
 "lint-staged": { 
    "./src/*.js": [ "yarn prettier --write", "eslint src/*.js" ] 
 } 
```
