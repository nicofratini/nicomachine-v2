# Vue 3 & Nuxt Development Patterns

## Component Design
- Use Composition API for all new components
- Implement proper prop validation with TypeScript
- Create reusable composables for shared logic
- Follow single responsibility principle for components

## State Management
- Use Pinia for complex state management
- Implement proper state normalization
- Handle async state with proper loading/error states
- Use local component state for simple scenarios

## Performance Optimization
- Implement proper lazy loading for routes and components
- Use v-memo for expensive computations
- Optimize images with Nuxt Image module
- Implement proper caching strategies for API calls

## Accessibility
- Use semantic HTML elements
- Implement proper ARIA attributes
- Ensure keyboard navigation support
- Test with screen readers

## Tailwind CSS Integration
- Use Nuxt Tailwind module for optimal integration
- Configure JIT mode for development and production
- Use Tailwind Typography for rich text content
- Implement proper CSS-in-JS patterns with Tailwind

### Component Structure with Tailwind
```vue
<template>
  <div class="container mx-auto px-4 sm:px-6 lg:px-8">
    <h1 class="text-3xl font-bold text-gray-900 dark:text-white">
      {{ title }}
    </h1>
  </div>
</template>

<script setup lang="ts">
interface Props {
  title: string
}

defineProps<Props>()
</script>
```

### Responsive Design Patterns
- Mobile-first approach with Tailwind breakpoints
- Use container queries where appropriate
- Implement proper touch targets (min 44px)
- Test across all breakpoint ranges