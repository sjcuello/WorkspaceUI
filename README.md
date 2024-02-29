# How to create a monorepo with pnpm and submodules

## Steps to create a monorepo with pnpm and submodules

1- Create a new repository

```bash
git init
```

2- Add submodules

```bash
git submodule add <repository-url> packages/<project-name>
```

3- Initialize and Update Submodules: Make sure all your submodules are initialized and updated.

```bash
git submodule update --init --recursive
```

4- Configure pnpm-workspace.yaml: At the root of your workspace repository, create or update the pnpm-workspace.yaml to include paths to your submodules.

```yml
packages:
  - packages/\*
```

5- Install pnpm: Install pnpm globally if you haven't already.

```bash
npm install -g pnpm
```

6- Init pnpm workspace

```bash
pnpm init
```

7- \*If you want packages within your workspace to depend on each other, you can simply add those dependencies in their respective package.json files using the package name. For example, if package-a depends on package-b, in package-a's package.json, you would add:

```json
"dependencies": {
  "package-b": "workspace:\*"
}
```

**Note:** keep in mind that you have to name the package in the package.json file, and the name should be the same as the folder name like this:

```json
{
  "name": "@workspaceui/componentlibrary",
  "version": "1.0.0",
  ...
}
```

and if it's a dependency in another package.json file, you should add it like this:

```json
{
  "dependencies": {
    "@workspaceui/componentlibrary": "workspace:*"
  }
}
```

8- Once all your packages are set up, go back to the root of your workspace and run:

```bash
pnpm install
```

9- To run scripts would use:

```bash
pnpm --filter @workspaceui/componentlibrary start
```

## Aditional commands:

- To update all submodules:

```bash
git submodule update --recursive --remote
```

- To install any library in a specific package (from the workspace root) run:

```bash
pnpm --filter @workspaceui/componentlibrary add @mui/utils
```

or navigate to the package folder and run:

```bash
pnpm add @mui/utils
```
