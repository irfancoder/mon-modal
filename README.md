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

| Props                 | Type          | Default                 | Description         |
| -------------         |-------------  | :-----------------:     | ---------------     |
| title                 | string        |  -                      | Title of the modal  |
| label                 | string        |  -                      | Button label for default modal implementation     |
| titleClass            | string        | 'mon-modal-title'       | Class for title (Tailwind compatible)             |
| labelClass            | string        |  -                      | Class for button label for default modal implementation (Tailwind compatible)   |
| backdropClass         | string        | 'mon-modal'             | Class for modal backdrop (Tailwind compatible)    |
| modalClass            | string        | 'mon-modal-container'   | Class for modal container (Tailwind compatible)   |
| headerClass           | string        | 'mon-modal-header'      | Class for modal header (Tailwind compatible)      |
| bodyClass             | string        | 'mon-modal-body'        | Class for modal body (Tailwind compatible)        |
| footerClass           | string        | 'mon-modal-footer'      | Class for modal footer (Tailwind compatible)      |
| persistent            | boolean       | false                   | Content rendered inside modal persists even when modal is closed. By default, the content rendered will be destroyed once user closes the modal     |
| disableClickAway      | boolean       | false                   | Disables modal close behavior when user interacts with out of modal content. By default, modal will close when user clicks away.      |
| disableEsc            | boolean       | false                   | Disables modal close behavior when user presses `Esc` key. By default, modal will close when user presses `Esc` key.    |
| openOnMount           | boolean       | false                   | Modal will open on `mounted()`. Refer to Vue's [mounted](https://vuejs.org/v2/api/#mounted) lifecycle for more information      |
| enter                 | string        | 'mon-modal-enter'       | Custom transition class for modal `enter` phase           |
| enterActive           | string        | 'mon-modal-enter-active'| Custom transition class for modal `enter-active` phase    |
| enterTo               | string        | 'mon-modal-enter-to'    | Custom transition class for modal `enter-to` phase        |
| leave                 | string        | 'mon-modal-leave'       | Custom transition class for modal `leave` phase           |
| leaveActive           | string        | 'mon-modal-leave-active'| Custom transition class for modal `leave-active` phase    |
| leaveTo               | boolean       | 'mon-modal-leave-to'    | Custom transition class for modal `leave-to` phase        |

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


<!-- Custom Transition Class -->
props: 
 * title
 * enter
 * enter-active
 * enter-to
 * leave
 * leave-active
 * leave-to
  <mon-modal [...props]>
   ...
  </mon-modal>
```
3. Component Lifecycle Hooks

If you need to do logic based on the modal's lifecycle, you can utilize the predefined hooks given below!

| Hooks                 | Type          | Description                     |
| -------------         |-------------  | -------------------             |
| before-open           | function      | Called before the modal opens   |
| after-open            | function      | Called after the modal opens    |
| before-close          | function      | Called before the modal closes  |
| after-close           | function      | Called after modal closes       |

Example Implementation
```
<mon-modal 
    @before-open="..."
    @after-open="..."
    @before-close="..."
    @after-close="...">
    ...
</mon-modal>
```
Check the [Demo](https://jsfiddle.net/irfancoder/6rcuwbq0/289/) on how to use modal lifecycle hooks


5. Handling Modal Behavior outside Usual Scope

There will be times, you will find yourselves needing to trigger modal behaviors outside of the normal scope (eg. clicking a button). MonModal provides two (2) internal functions that can be accessed through Vue's `ref="..." & $refs`.

The two functions are:

- openModal()
- closeModal()

Check the [Demo](https://jsfiddle.net/irfancoder/6rcuwbq0/289/) on how to use modal's internal functions


<!-- LICENSE -->
## License
[MIT License](https://github.com/irfancoder/mon-modal/blob/master/LICENSE)

<!-- CONTACT -->
## Author

Irfan Ismail - [@irfancoder](https://twitter.com/irfancoder) - irfan.ismail96@gmail.com
