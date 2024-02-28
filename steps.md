How to create a monorepo with pnpm and submodules

1- Create a new repository
git init

2- Add submodules

git submodule add <repository-url> packages/<project-name>

3- Initialize and Update Submodules: Make sure all your submodules are initialized and updated.
git submodule update --init --recursive

4- Configure pnpm-workspace.yaml: At the root of your workspace repository, create or update the pnpm-workspace.yaml to include paths to your submodules.

packages:

- packages/\*

5- Install pnpm: Install pnpm globally if you haven't already.

npm install -g pnpm

6- Init pnpm workspace

pnpm init

7- \*If you want packages within your workspace to depend on each other, you can simply add those dependencies in their respective package.json files using the package name. For example, if package-a depends on package-b, in package-a's package.json, you would add:

"dependencies": {
"package-b": "workspace:\*"
}

8- Once all your packages are set up, go back to the root of your workspace and run:

pnpm install

9- To run scripts would use:

pnpm run test -r
