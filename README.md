# mon-modal

MonModal a feature-rich modal Vue2 component. It focuses on bringing the best of Vue's features to achieve common &amp; advanced behavior patterns while giving you the freedom to style the component to your liking. Built-to-work with <a href="https://tailwindcss.com/">TailwindCSS</a>.

![mon-modal-gif](https://github.com/irfancoder/mon-modal/blob/master/asset/mon-modal.gif)

[Demo](https://jsfiddle.net/irfancoder/6rcuwbq0/289/)
<!-- GETTING STARTED -->
## Getting Started 

```
// npm
npm i @irfanismail/mon-modal

// yarn
yarn add @irfanismail/mon-modal
```


<!-- USAGE EXAMPLES -->
## Usage 

1. Table of Props

| Props                 | Type          | Default               |
| -------------         |-------------  | :-----------------:   |
| title                 | string        |                       |
| label                 | string        |                       |
| titleClass            | string        | 'mon-modal-title'     |
| labelClass            | string        |                       |
| backdropClass         | string        | 'mon-modal'           |
| modalClass            | string        | 'mon-modal-container' |
| headerClass           | string        | 'mon-modal-header'    |
| bodyClass             | string        | 'mon-modal-body'      |
| footerClass           | string        | 'mon-modal-footer'    |
| persistent            | boolean       | false                 |
| disableClickAway      | boolean       | false                 |
| disableEsc            | boolean       | false                 |
| openOnMount           | boolean       | false                 |

2. Combinations of Slots & Props
```
<!-- Basic Modal -->
props: 
* title
* label 
  <mon-modal [...props]>
      <template #body>...</template>
      <template #footer="{ close }">...</template>
  </mon-modal>
  
<!-- Custom Header & Content -->
props: 
* label 
  <mon-modal [...props]>
    <template #header="{ close }">...</template>
    <template #custom="{ open, close }">...</template>
  </mon-modal>

<!-- Custom Trigger -->
props: 
 * title
  <mon-modal [...props]>
    <template #trigger="{ open }"></template>
    <template #body>...</template>
  </mon-modal>

  
```
3. Lifecycle Hooks
| Hooks                 | Type          |
| -------------         |-------------  |
| before-open           | function      |
| after-open            | function      |
| before-close          | function      |
| after-close           | function      |

Check the [Demo](https://jsfiddle.net/irfancoder/6rcuwbq0/289/) on how to use modal lifecycle hooks

5. Handling Modal Behavior outside Usual Scope

There will be times, you will find yourselves needing to trigger modal behaviors outside of the normal scope (eg. clicking a button). MonModal provides two (2) internal functions that can be accessed through Vue's `ref="..." & $refs`.

The two functions are:

- openModal()
- closeModal()

Check the [Demo](https://jsfiddle.net/irfancoder/6rcuwbq0/289/) on how to use modal's internal functions


<!-- ROADMAP -->
## Roadmap 

TODO: 
- Improve Base styling
- Add Base Transition Animation
- Allow Custom Transition Animation

<!-- LICENSE -->
## License


<!-- CONTACT -->
## Contact

Irfan Ismail - [@irfancoder](https://twitter.com/irfancoder) - irfan.ismail96@gmail.com
