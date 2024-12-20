# Usando o vee-validate

# Formulário de Login com Validação usando Vee-Validate

Este é um exemplo de um formulário de login criado utilizando Vue.js, TailwindCSS, e a biblioteca de validação Vee-Validate com Yup para o esquema de validação.

## Pré-requisitos

Certifique-se de ter o Node.js instalado. Você também precisará de um projeto Vue.js com TailwindCSS configurado. Para instalar as dependências adicionais, utilize os comandos abaixo:

```bash
npm install vee-validate yup
```

ou

```bash
yarn add vee-validate yup
```

## Código do Componente

Aqui está o código completo do componente:

```vue
<script setup lang="ts">
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Card } from './components/ui/card';
import { Toaster } from './components/ui/sonner';
import CardFooter from './components/ui/card/CardFooter.vue';
import { toast } from 'vue-sonner';
import { useForm, useField } from 'vee-validate';
import * as yup from 'yup';

// Definindo o esquema de validação
const schema = yup.object({
  email: yup.string().required('Email é obrigatório').email('Email inválido'),
  password: yup.string().required('Senha é obrigatória'),
});

// Usando o useForm para gerenciar o estado do formulário
const { handleSubmit, resetForm } = useForm({
  validationSchema: schema,
});

// Usando useField para gerenciar os campos
const { value: email, errorMessage: emailError } = useField('email');
const { value: password, errorMessage: passwordError } = useField('password');

const handleLogin = handleSubmit(() => {
  toast.success("Login realizado com sucesso");
  resetForm();
});
</script>

<template>
  <div class="flex items-center justify-center min-h-screen bg-background text-foreground">
    <Toaster />
    <Card class="w-full max-w-md p-6 bg-card">
      <CardHeader>
        <CardTitle class="text-center text-xl font-bold">Login</CardTitle>
      </CardHeader>
      <CardContent>
        <form @submit="handleLogin">
          <div class="mb-4">
            <label for="email" class="block text-sm mb-1">Email</label>
            <Input 
              id="email" 
              type="email"
              placeholder="Digite seu email"
              class="bg-input text-foreground border border-border focus:ring-0 focus:outline-none"
              v-model="email"
            />
            <span class="text-red-500 text-sm">{{ emailError }}</span>
          </div>
          <div class="mb-6">
            <label for="password" class="block text-sm mb-1">Senha</label>
            <Input 
              id="password" 
              type="password"
              placeholder="Digite sua senha"
              class="bg-input text-foreground border border-border focus:ring-0 focus:outline-none"
              v-model="password"
            />
            <span class="text-red-500 text-sm">{{ passwordError }}</span>
          </div>
          <Button 
            type="submit"
            class="w-full bg-primary text-primary-foreground border border-border hover:bg-secondary focus:ring-0 focus:outline-none px-6 py-4"
          >
            Entrar
          </Button>
        </form>
      </CardContent>
      <CardFooter class="text-center text-sm">
        <p>Não tem uma conta? <a href="/register" class="text-accent hover:underline">Cadastre-se</a></p>
      </CardFooter>
    </Card>
  </div>
</template>
```

## Explicação do Código

### Importações
- **Componentes personalizados:** Importamos componentes reutilizáveis como `Button`, `Input`, `Card`, entre outros.
- **Vee-Validate:** Importamos `useForm`, `useField` do `vee-validate` e definimos o esquema de validação com `yup`.

### Esquema de Validação
Utilizamos o `yup` para definir regras para os campos de email e senha:
- **Email:** Obrigatório e deve ser um email válido.
- **Senha:** Obrigatória.

### Gerenciamento de Campos
- `useField` é usado para gerenciar valores e mensagens de erro dos campos.
- As mensagens de erro são exibidas abaixo dos campos se houver problemas na validação.

### Submissão do Formulário
O método `handleLogin` é chamado ao enviar o formulário. Ele exibe uma mensagem de sucesso usando o `vue-sonner` e reseta o formulário após a submissão bem-sucedida.

## Estilização
Os estilos foram ajustados para o tema Dracula, com configurações de cores e classes personalizadas definidas no TailwindCSS.

## Resultado Final
Este componente apresenta um formulário de login funcional com validação, estilizado com TailwindCSS e integrando o tema Dracula.





This template should help get you started developing with Vue 3 and TypeScript in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

Learn more about the recommended Project Setup and IDE Support in the [Vue Docs TypeScript Guide](https://vuejs.org/guide/typescript/overview.html#project-setup).
