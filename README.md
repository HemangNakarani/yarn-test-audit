# Issue Reproduction Steps

- Clone this repo
- run `yarn install`
- run `yarn npm audit  --environment production --all --recursive --no-deprecations`, you should get vulnerability reported `@babel/traverse` - it is devDep of `@hemangjs/modules`, which is dep in `main-app`
- now change **dependencies** to **devDependencies** in `main-app/package.json` and run `yarn install`
- again run above audit command and it would not report any vulnerability


As a conclusion, yarn audit only exclude top level devDependencies in prod mode

We can verify the same in yarn audit code https://github1s.com/yarnpkg/berry/blob/master/packages/plugin-npm-cli/sources/npmAuditUtils.ts - checkout functions `getTopLevelDependencies` and `getPackages`
