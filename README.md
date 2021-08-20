# Vue.js Pagination
A simple Vue.js component that helps to print and handle a pagination

- [Vue.js Pagination](#vuejs-pagination)
  - [Installation](#installation)
  - [Usage](#usage)
  - [Example](#example)
  - [Props](#props)
  - [Events](#events)

## Installation
First, you must run `npm install @2alheure/vue-pagination`.  
Then, you can import it with `import Pagination from "@2alheure/vue-pagination";`.

## Usage
Call the component with two things:
- a `v-model` directive, using a variable representing the active page (integer)
- a `maxPage` prop (integer) representing the max page number

## Example
```html
<Pagination v-model="page" :maxPage="10" />

<script>
  import Pagination from "@2alheure/vue-pagination";
  
  export default {
    components: {
      Pagination
    },
    data() {
      return {
        page: 3
      }
    }
  };
</script>
```

## Props
| Name                     |  Type  | Default value | Description                                                            |
| :----------------------- | :----: | :-----------: | ---------------------------------------------------------------------- |
| modelValue               | Number |     none      | The prop linked to the `v-model` directive (mandatory).                |
| maxPage                  | Number |     none      | The maximum number of pages (mandatory).                               |
| textColor                | String |   `#4a5568`   | The color of the buttons' text.                                        |
| backgroundColor          | String |    `#fff`     | The color of the buttons' background.                                  |
| borderColor              | String |   `#e2e8f0`   | The color of the buttons' borders.                                     |
| selectedTextColor        | String |   `#f7fafc`   | The color of the text for the selected button.                         |
| selectedBackgroundColor  | String |   `#4a5568`   | The color of the background for the selected button.                   |
| selectedBorderColor      | String |   `#e2e8f0`   | The color of the borders for the selected button.                      |
| hoverTextColor           | String |   `#f7fafc`   | The color of the text for the hovered button.                          |
| hoverBackgroundColor     | String |   `#a0aec0`   | The color of the background for the hovered button.                    |
| hoverBorderColor         | String |   `#e2e8f0`   | The color of the borders for the hovered button.                       |
| controlsHoverBorderColor | String |   `#cbd5e0`   | The color of the borders for the hovered "Previous" or "Next" buttons. |

## Events
| Name              | Value type |          Value           | Description                                   |
| :---------------- | :--------: | :----------------------: | --------------------------------------------- |
| update:modelValue |   Number   |     The page clicked     | Emitted each time the page changes            |
| prev              |   Number   | The previous page number | Emitted when the "Previous" button is clicked |
| next              |   Number   |   The next page number   | Emitted when the "Next" button is clicked     |
