# Vue JS Pagination
A simple pagination component for Vue JS

## How to use
Download the component file and place it in your `components/` folder.  
Then, you can import it with `import Pagination from "@/components/Pagination.vue";`.  
Use it then by calling `<Pagination v-model="foo" :maxPage="bar" />` where foo is the current page number (please note the `v-model` directive).

## Props
You must pass a `maxPage` prop, which is an integer indicating the total number of pages that exist.

## Example
```html
<Pagination v-model="page" :maxPage="10" />

<script>
  import Pagination from "@/components/Pagination.vue";
  
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
