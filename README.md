# Passo a Passo para Configurar ShadCN + Vite + Vue + Tailwind CSS

---

## 1. Criar um novo projeto com Vite
```bash
npm create vite@latest my-shadcn-vue-app -- --template vue
cd my-shadcn-vue-app
```

---

## 2. Instalar as dependências
```bash
npm install
```

---

## 3. Instalar o Tailwind CSS
```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init
```

---

## 4. Configurar o Tailwind
Substituir o conteúdo do arquivo `tailwind.config.js` com:
```js
const animate = require("tailwindcss-animate");

/** @type {import('tailwindcss').Config} */
module.exports = {
  darkMode: ["class"],
  safelist: ["dark"],
  content: [
    "./index.html",
    "./src/**/*.{vue,js,ts,jsx,tsx}",
    "./components/**/*.{vue,js,ts,jsx,tsx}",
    "./pages/**/*.{vue,js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {
      colors: {
        border: "hsl(var(--border))",
        input: "hsl(var(--input))",
        ring: "hsl(var(--ring))",
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))",
        },
        secondary: {
          DEFAULT: "hsl(var(--secondary))",
          foreground: "hsl(var(--secondary-foreground))",
        },
        destructive: {
          DEFAULT: "hsl(var(--destructive))",
          foreground: "hsl(var(--destructive-foreground))",
        },
        muted: {
          DEFAULT: "hsl(var(--muted))",
          foreground: "hsl(var(--muted-foreground))",
        },
        accent: {
          DEFAULT: "hsl(var(--accent))",
          foreground: "hsl(var(--accent-foreground))",
        },
        popover: {
          DEFAULT: "hsl(var(--popover))",
          foreground: "hsl(var(--popover-foreground))",
        },
        card: {
          DEFAULT: "hsl(var(--card))",
          foreground: "hsl(var(--card-foreground))",
        },
      },
      borderRadius: {
        xl: "calc(var(--radius) + 4px)",
        lg: "var(--radius)",
        md: "calc(var(--radius) - 2px)",
        sm: "calc(var(--radius) - 4px)",
      },
      keyframes: {
        "accordion-down": {
          from: { height: 0 },
          to: { height: "var(--radix-accordion-content-height)" },
        },
        "accordion-up": {
          from: { height: "var(--radix-accordion-content-height)" },
          to: { height: 0 },
        },
      },
      animation: {
        "accordion-down": "accordion-down 0.2s ease-out",
        "accordion-up": "accordion-up 0.2s ease-out",
      },
    },
  },
  plugins: [animate],
};
```

---

## 5. Configurar o arquivo CSS
Crie ou edite o arquivo `src/index.css` e adicione:
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

/* Definir tema Dracula */
:root {
  --background: #282a36;
  --foreground: #f8f8f2;
  --border: #6272a4;
  --input: #44475a;
  --ring: #bd93f9;
  --primary: #bd93f9;
  --primary-foreground: #ffffff;
  --secondary: #6272a4;
  --secondary-foreground: #f8f8f2;
  --accent: #50fa7b;
  --accent-foreground: #282a36;
  --muted: #44475a;
  --muted-foreground: #f8f8f2;
  --destructive: #ff5555;
  --destructive-foreground: #f8f8f2;
  --card: #44475a;
  --card-foreground: #f8f8f2;
  --radius: 0.5rem;
}
```

---

## 6. Instalar dependências do ShadCN
```bash
npm install class-variance-authority clsx tailwind-merge
```

---

## 7. Criar componentes ShadCN
Exemplo de botão em `src/components/ui/button.vue`:
```vue
<script setup lang="ts">
import { cn } from '@/lib/utils';

defineProps({
  variant: {
    type: String,
    default: 'default',
  },
  class: {
    type: String,
    default: '',
  },
});
</script>

<template>
  <button
    :class="cn(
      'inline-flex items-center justify-center px-4 py-2 border rounded-md font-medium shadow-sm focus:outline-none',
      variant === 'primary' && 'bg-primary text-primary-foreground',
      variant === 'secondary' && 'bg-secondary text-secondary-foreground',
      class
    )"
  >
    <slot />
  </button>
</template>
```

---

## 8. Executar o projeto
```bash
npm run dev
