# PatternFly React Component Groups

This repo contains a set of opinionated react component groups used to standardize functionality and look and feel across products.  The components are based of PatternFly with some additional functionality. 

## Contribution guide

### Before adding a new component:
- make sure your use case is new/complex enough to be added to this extension
- the component should bring a value value above and beyond existing PatternFly components

### To add a new component:
1. create a folder in `src/` matching its name (for example `src/MyNewComponent`)
2. to the new folder add a new `.tsx` file named after the component (for example `src/MyNewComponent/MyNewComponent.tsx`)
3. to the same folder include also a `index.ts` which will export the component as a default and then all necessary interfaces
4. don't forget to export your component using `export * from './ComponentName'` from the root `index` file located in `src/index.ts`

#### Example component:
```
import * as React from 'react';
import { Text } from '@patternfly/react-core';
import { createUseStyles } from 'react-jss';

// do not forget to export your component's interface
// always place component's interface above the component itself in the code
export interface MyNewComponentProps {
  text: String;
}

const useStyles = createUseStyles({
  myText: {
    fontFamily: 'monospace',
    fontSize: 'var(--pf-v5-global--icon--FontSize--md)',
  },
})

// do not use named export of your component, just a default one
const MyNewComponent: React.FunctionComponent<MyNewComponentProps> = () => {
  const classes = useStyles();

  return (
    <Text className={classes.myText}>
      This is my new reusable component
    </Text>
  );
};

export default MyNewComponent;
``` 

#### Index file example:
```
export { default } from './MyNewComponent';
export * from './MyNewComponent';
``` 

#### Component directory structure example:
```
src
|- MyNewComponent
|  |- index.ts
|  |- MyNewComponent.tsx
|- ...
|- ...
|- ...
|- index.ts       <<-- export * from './MyNewComponent';
``` 

### Component's API rules:
- prop names comply with PatternFly components naming standards (`variant`, `onClick`, `position`, etc.)
- the API is maximally simplified and all props are provided with a description
- it is build on the top of existing PatternFly types without prop omitting
- it is well documented using the PatternFly documentation (`/packages/module/patternfly-docs/content/extensions/component-groups/examples/MyNewComponent/MyNewComponent.md`) with examples of all possible use cases (`packages/module/patternfly-docs/content/extensions/component-groups/examples/MyNewComponent/MyNewComponent[...]Example.tsx`)
- do not unnecessarily use external libraries in your component - rather, delegate the necessary logic to the component's user using the component's API

#### Component API definition example:
```
// when possible, extend available PatternFly types
export interface MyNewComponentProps extends ButtonProps {
    customLabel: Boolean
};

export const MyNewComponent: React.FunctionComponent<MyNewComponentProps> = ({ customLabel, ...props }) => ( ... );
```


#### Markdown file example:
```
---
section: extensions
subsection: Component groups
id: MyNewComponent
propComponents: ['MyNewComponent']
---

import MyNewComponent from "@patternfly/react-component-groups/dist/dynamic/MyNewComponent";

## Component usage

MyNewComponent has been created to demo contributing to this repository.

### MyNewComponent component example label

```js file="./MyNewComponentExample.tsx"```

```

#### Component usage file example: (`MyNewComponentExample.tsx`)
```
import React from 'react';

const MyNewComponentExample: React.FunctionComponent = () => (
  <MyNewComponent customLabel="My label">
);

export default BatteryLowExample;
```

### Sub-components:
When adding a component for which it is advantageous to divide it into several sub-components make sure: 
- component and all its sub-components are located in separate files and directories straight under the `src/` folder
- sub-components are exported and documented separately from their parent
- parent component should provide a way to pass props to all its sub-components

The aim is to enable the user of our "complex" component to use either complete or take advantage of its sub-components and manage their composition independently.

### Testing:
When adding/making changes to a component, always make sure your code is tested:
- use React Testing Library for testing 
- add tests to a `[ComponentName].test.tsx` file to your component's directory
- make sure all the core logic is covered

### Styling:
- for styling always use JSS
- new classNames should match PatternFly conventions (`pf-cg-[component]-[more-details]`)
- new CSS variables should be named like `--pf-cg-[my-variable]-[more-details]`

## Building for production

- run npm install
- run npm run build

## Development
- run npm install
- run npm run start to build and start the development server

## Testing and Linting
- run npm run test to run the tests for the demo component
- run npm run lint to run the linter

## A11y testing

- run npm run build:docs followed by npm run serve:docs, then run npm run test:a11y in a new terminal window to run our accessibility tests for the components. Once the accessibility tests have finished running you can run 
- npm run serve:a11y to locally view the generated report.

