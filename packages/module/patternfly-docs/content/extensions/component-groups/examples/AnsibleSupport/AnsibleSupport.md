---
# Sidenav top-level section
# should be the same for all markdown files
section: Component groups
subsection: Status and state indicators
# Sidenav secondary level section
# should be the same for all markdown files
id: Ansible support
# Tab (react | react-demos | html | html-demos | design-guidelines | accessibility)
source: react
# If you use typescript, the name of the interface to display props for
# These are found through the sourceProps function provided in patternfly-docs.source.js
propComponents: ['AnsibleSupport']
sourceLink: https://github.com/patternfly/react-component-groups/blob/main/packages/module/patternfly-docs/content/extensions/component-groups/examples/AnsibleSupport/AnsibleSupport.md
---

import AnsibleSupport from '@patternfly/react-component-groups/dist/dynamic/AnsibleSupport';

The **Ansible support** component displays the Ansible project logo, with a support status style.

### Ansible supported

By default, the Ansible logo displays as normal and in full color, meaning that it is supported. 

```js file="./AnsibleSupportedExample.tsx"

```

### Ansible unsupported

To specify that Ansible is not supported, set the `isSupported` property to `false`.

```js file="./AnsibleUnsupportedExample.tsx"

```