# Virtual Scroll Component

This is a Vue 3 virtual scroll component designed to efficiently render a large list of items. It uses virtualization techniques to display only the visible portion of the list, improving performance for large datasets.

## Features

- **Virtual Scrolling**: Renders only the visible items.
- **Customizable**: Accepts `itemHeight` and supports scoped slots for custom item rendering.
- **Performance-Optimized**: Handles large datasets with smooth scrolling.

## Usage

1. Import the component into your project.
2. Pass the list data and use the `item` slot to define how each item should be rendered.

### Example

```vue
<VirtualScroll :list="items" :itemHeight="50">
  <template #item="{ data }">
    <div>{{ data.value }}</div>
  </template>
</VirtualScroll>
```

### Setup Instructions

```
git clone <repository_url>
```

```
npm install
```

```
npm run dev
```

### Props

- `list`: The array of items to be displayed.
- `itemHeight`: The height of each item in the list.
- `item`: A scoped slot for custom rendering of each item.

| Prop       | Type   | Default | Description                    |
| ---------- | ------ | ------- | ------------------------------ |
| list       | Array  | `[]`    | Array of data to render.       |
| itemHeight | Number | `50`    | Height of each item in pixels. |

### Slots

- `item`: A scoped slot for custom rendering of each item.

## Contributing

Contributions are welcome! Please fork the repository, make your changes, and submit a pull request.

### License

This project is licensed under the MIT License.
