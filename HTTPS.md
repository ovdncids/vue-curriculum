# HTTPS localhost 인증서
```sh
npm install -D @vitejs/plugin-basic-ssl
```

vite.config.ts
```ts
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import basicSsl from '@vitejs/plugin-basic-ssl'

export default defineConfig({
  plugins: [
    vue(),
    basicSsl()
  ],
  server: {
    host: 'localhost',
    port: 3000
  }
})
```
