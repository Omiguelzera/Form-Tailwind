<script setup lang="ts">
  import { Button } from '@/components/ui/button'
  import { Input } from '@/components/ui/input'
  import { Card } from './components/ui/card';
  import { Toaster } from './components/ui/sonner';
  import CardFooter from './components/ui/card/CardFooter.vue';
  import { toast } from 'vue-sonner';

const handleLogin = () =>{
  toast.success("Login realizado com sucesso");
};
</script>


<template>
    <div claas="flex items-center justify-center min-h-screen bg-background text-foreground">
      <Toaster />
      <Card class="w-full max-w-md p-6 bg-card">
        <CardHeader>
            <CardTitle class="text-center text-xl font-bold">Login</CardTitle>
        </CardHeader>
        <CardContent>
          <form>
            <div>
              <label for="email" class="block text-sm mb">Email</label>
              <Input 
              id="email" 
              type="email"
              placeholder="Digite seu email"
              class="bg-input text-foreground border border-border  focus:ring-0 focus:outline-none"
              />
            </div>
            <div>
              <label for="password" class="block text-sm mb-1">Senha</label>
              <Input 
              id="password" 
              type="password"
              placeholder="Digite sua senha"
              class="bg-input text-foreground border border-border focus:ring-0 focus:outline-none"
              />
            </div>
            <Button 
            @click="handleLogin"
            type="submit"
            class="w-full bg-primary text-primary-foreground border border-border hover:bg-secondary focus:ring-0 focus:outline-none px-6 py-4 mt-6 "
            > Entrar</Button>
          </form>
        </CardContent>
        <CardFooter class="text-center text-sm">
          <p> Não tem uma conta ? <a href="/register" class="text-accent" hover:underline>Cadastre-se</a></p>
        </CardFooter>
      </Card>
    </div>
</template>
