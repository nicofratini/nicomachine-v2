# UI/UX Standards with Tailwind CSS

## Tailwind Design System

### Color Palette
```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#eff6ff',
          500: '#3b82f6',
          900: '#1e3a8a'
        },
        gray: {
          50: '#f9fafb',
          500: '#6b7280',
          900: '#111827'
        }
      }
    }
  }
}
```

### Typography Scale
- Use Tailwind's typography scale: text-xs to text-9xl
- Implement consistent line heights with leading utilities
- Use font-weight utilities: font-normal, font-medium, font-semibold, font-bold
- Custom font families via Tailwind config when needed

### Spacing System
- Use Tailwind's spacing scale (4px increments)
- Consistent padding: p-2, p-4, p-6, p-8 for different contexts
- Margin utilities: m-2, m-4, m-6, m-8 for spacing between elements
- Gap utilities for flexbox and grid layouts

## Component Patterns

### Button System
- Create a comprehensive, reusable button system that intelligently chooses between <button>, <a>, and <NuxtLink> elements based on usage context.
- Use dynamic component rendering with <component :is="componentTag">
- Implement conditional logic to determine the appropriate HTML element
- Support all button variants, sizes, and states
- Handle accessibility attributes properly for each element type
```javascript
// Conditional logic for element selection
const componentTag = computed(() => {
  if (props.to) return 'NuxtLink'           // Internal routing
  if (props.href) return 'a'                // External links
  return 'button'                           // Default interactive element
})
```

```typescript
interface ButtonProps {
  // Element determination
  to?: string                    // NuxtLink internal routing
  href?: string                  // External URL
  
  // Button variants
  variant?: 'primary' | 'secondary' | 'outline' | 'ghost' | 'danger'
  size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl'
  
  // States
  loading?: boolean
  disabled?: boolean
  
  // Icons
  iconLeft?: string
  iconRight?: string
  iconOnly?: boolean
  
  // Link-specific props
  target?: '_blank' | '_self' | '_parent' | '_top'
  rel?: string
  external?: boolean             // Force external link behavior
  
  // Accessibility
  ariaLabel?: string
  
  // Button-specific
  type?: 'button' | 'submit' | 'reset'
}
```

- Create base button classes that work across all element types
- Implement size variations (padding, font-size, icon sizing)
- Add state classes (hover, focus, disabled, loading)
- Ensure consistent visual appearance regardless of underlying element
- Maintain accessiblity for (type attribute, aria-label, aria-disabled...)

### Card Components
```vue
<UiCard>
  <UiCardHeader>
    <UiCardTitle>Card Title</UiCardTitle>
  </UiCardHeader>
  <UiCardContent>
    <p>Card content goes here</p>
  </UiCardContent>
</UiCard>
```

### Form Elements
```vue
  <UiLabel for="email">Email</UiLabel>
  <UiInput 
    id="email"
    type="email" 
    placeholder="Enter your email"
    v-model="form.email"
  />
</div>
```

## Responsive Design with Tailwind

### Breakpoint Strategy
- Mobile First: Design for mobile, enhance for larger screens
- Breakpoints: sm (640px), md (768px), lg (1024px), xl (1280px), 2xl (1536px)
- Use responsive prefixes: `sm:text-lg md:text-xl lg:text-2xl`

### Grid System
```vue
<!-- Responsive Grid -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
  <div class="col-span-1">Item 1</div>
  <div class="col-span-1">Item 2</div>
  <div class="col-span-1">Item 3</div>
</div>

<!-- Responsive Flexbox -->
<div class="flex flex-col md:flex-row gap-4">
  <div class="flex-1">Content</div>
  <div class="w-full md:w-64">Sidebar</div>
</div>
```

## Dark Mode Implementation

### Dark Mode Setup
```js
// nuxt.config.ts
export default defineNuxtConfig({
  css: ['~/assets/css/main.css'],
  modules: ['@nuxtjs/tailwindcss'],
  tailwindcss: {
    config: {
      darkMode: 'class',
    }
  }
})
```

### Dark Mode Patterns
```vue
<!-- components/ThemeToggle.vue -->
<template>
  <div class="theme-toggle">
    <UiButton
      variant="ghost"
      size="sm"
      @click="toggleTheme"
      :aria-label="buttonLabel"
      class="relative"
    >
      <Icon 
        :name="currentIcon" 
        class="h-4 w-4 transition-transform duration-200"
        :class="{ 'rotate-180': $colorMode.value === 'dark' }"
      />
      <span class="sr-only">{{ buttonLabel }}</span>
    </UiButton>
  </div>
</template>

<script setup lang="ts">
const { $colorMode } = useNuxtApp()

const currentIcon = computed(() => {
  switch ($colorMode.value) {
    case 'light':
      return 'sun'
    case 'dark':
      return 'moon'
    default:
      return 'monitor'
  }
})

const buttonLabel = computed(() => {
  switch ($colorMode.value) {
    case 'light':
      return 'Switch to dark mode'
    case 'dark':
      return 'Switch to light mode'
    default:
      return 'Switch to system theme'
  }
})

const toggleTheme = () => {
  const themes = ['light', 'dark', 'system']
  const currentIndex = themes.indexOf($colorMode.value)
  const nextIndex = (currentIndex + 1) % themes.length
  $colorMode.preference = themes[nextIndex]
}
</script>
```

```vue
<!-- Example component with dark mode styling -->
<template>
  <div class="app-container">
    <!-- Header -->
    <header class="bg-white dark:bg-gray-900 border-b border-gray-200 dark:border-gray-800">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex justify-between items-center py-4">
          <h1 class="text-2xl font-bold text-gray-900 dark:text-white">
            My App
          </h1>
          <ThemeToggle />
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <main class="min-h-screen bg-gray-50 dark:bg-gray-900">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
        <!-- Content Cards -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <UiCard class="hover:shadow-lg dark:hover:shadow-gray-800/25 transition-shadow">
            <UiCardHeader>
              <UiCardTitle class="text-gray-900 dark:text-gray-100">
                Card Title
              </UiCardTitle>
              <UiCardDescription class="text-gray-600 dark:text-gray-400">
                Card description text
              </UiCardDescription>
            </UiCardHeader>
            <UiCardContent>
              <p class="text-gray-700 dark:text-gray-300">
                Card content goes here
              </p>
            </UiCardContent>
          </UiCard>
        </div>
      </div>
    </main>
  </div>
</template>

```

## Animation and Interactions

### Micro-interactions
```vue
<!-- Hover Effects -->
<div class="
  transform hover:scale-105 
  transition-transform duration-200 ease-in-out
  hover:shadow-lg
">
  Hoverable Card
</div>

<!-- Loading States -->
<div class="animate-pulse">
  <div class="h-4 bg-gray-300 rounded w-3/4 mb-2"></div>
  <div class="h-4 bg-gray-300 rounded w-1/2"></div>
</div>

<!-- Focus States -->
<button class="
  focus:outline-none 
  focus:ring-2 focus:ring-primary-500 focus:ring-offset-2
  focus-visible:ring-2
">
  Accessible Button
</button>
```

## Accessibility with Tailwind

### Color Contrast
- Use Tailwind's color combinations that meet WCAG AA standards
- Test contrast ratios with tools like WebAIM
- Provide alternative indicators beyond color

### Focus Management
- Always include focus styles with focus:ring utilities
- Use focus-visible for keyboard-only focus
- Implement proper focus trapping in modals

### Screen Reader Support
```vue
<!-- Accessible Form -->
<div>
  <label for="email" class="sr-only">Email Address</label>
  <input 
    id="email"
    type="email"
    aria-describedby="email-help"
    class="..."
  />
  <p id="email-help" class="text-sm text-gray-600">
    We'll never share your email
  </p>
</div>
```

## Performance Optimization

### Bundle Size Optimization
- Configure Tailwind purging for production
- Use dynamic imports for large components
- Implement proper tree-shaking

### CSS Organization
```css
/* components/Button.vue */
<style scoped>
.btn-primary {
  @apply px-4 py-2 bg-primary-500 text-white rounded-lg font-medium;
  @apply hover:bg-primary-600 focus:ring-2 focus:ring-primary-500;
  @apply transition-colors duration-200;
}
</style>
```

### Custom Tailwind Components
```js
// tailwind.config.js
module.exports = {
  plugins: [
    function({ addComponents }) {
      addComponents({
        '.btn': {
          padding: '.5rem 1rem',
          borderRadius: '.375rem',
          fontWeight: '500',
        },
        '.btn-primary': {
          backgroundColor: '#3b82f6',
          color: '#ffffff',
          '&:hover': {
            backgroundColor: '#2563eb',
          },
        },
      })
    }
  ]
}
