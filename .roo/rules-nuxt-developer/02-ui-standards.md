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
```vue
<!-- Primary Button -->
<button class="
  px-4 py-2 
  bg-primary-500 hover:bg-primary-600 
  text-white font-medium 
  rounded-lg 
  transition-colors duration-200
  focus:outline-none focus:ring-2 focus:ring-primary-500 focus:ring-offset-2
  disabled:opacity-50 disabled:cursor-not-allowed
">
  Primary Action
</button>

<!-- Secondary Button -->
<button class="
  px-4 py-2 
  border border-gray-300 hover:border-gray-400 
  text-gray-700 font-medium 
  rounded-lg 
  transition-colors duration-200
  focus:outline-none focus:ring-2 focus:ring-gray-500 focus:ring-offset-2
">
  Secondary Action
</button>
```

### Card Components
```vue
<div class="
  bg-white dark:bg-gray-800 
  rounded-lg shadow-sm border border-gray-200 dark:border-gray-700
  p-6
  hover:shadow-md transition-shadow duration-200
">
  <h3 class="text-lg font-semibold text-gray-900 dark:text-white mb-2">
    Card Title
  </h3>
  <p class="text-gray-600 dark:text-gray-400">
    Card content goes here
  </p>
</div>
```

### Form Elements
```vue
<!-- Input Field -->
<div class="space-y-1">
  <label class="block text-sm font-medium text-gray-700 dark:text-gray-300">
    Email
  </label>
  <input 
    type="email"
    class="
      w-full px-3 py-2
      border border-gray-300 dark:border-gray-600
      rounded-md shadow-sm
      focus:ring-2 focus:ring-primary-500 focus:border-primary-500
      dark:bg-gray-700 dark:text-white
      placeholder-gray-400 dark:placeholder-gray-500
    "
    placeholder="Enter your email"
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
<!-- Light/Dark Mode Toggle -->
<button @click="toggleDarkMode" class="
  p-2 rounded-lg
  bg-gray-100 dark:bg-gray-800
  text-gray-800 dark:text-gray-200
  hover:bg-gray-200 dark:hover:bg-gray-700
  transition-colors duration-200
">
  <Icon :name="isDark ? 'sun' : 'moon'" />
</button>

<!-- Dark Mode Color Usage -->
<div class="
  bg-white dark:bg-gray-900
  text-gray-900 dark:text-white
  border-gray-200 dark:border-gray-700
">
  Content that adapts to theme
</div>
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