### Guia: Criando o Backend de um Carrinho de Compras ☕️🛒

Esse guia vai te orientar passo a passo na construção de um backend para um sistema de carrinho de compras utilizando **Node.js**, **Express**, **SQLite** e **Sequelize**. Vamos abordar desde o básico até funcionalidades extras, com dicas práticas e sugestões de melhorias! 🚀

---

### **1. Inicializando o Projeto 🌱**
1. **Crie o diretório do projeto**:
   ```bash
   mkdir coffee-shop-backend
   cd coffee-shop-backend
   ```
2. **Inicie o projeto com npm**:
   ```bash
   npm init -y
   ```
3. **Instale as dependências**:
   ```bash
   npm install express sqlite3 sequelize bcrypt jsonwebtoken dotenv cors body-parser
   npm install --save-dev nodemon
   ```
   - 🔑 **Dica**: Use o `nodemon` para reiniciar automaticamente o servidor durante o desenvolvimento. Adicione um script no `package.json`:
     ```json
     "scripts": {
       "dev": "nodemon index.js"
     }
     ```

---

### **2. Configurando o Banco de Dados 📦**
1. Crie o arquivo `config/database.js` para configurar o **SQLite**:
   - **Dica**: Use `sequelize.sync({ force: true })` no início para testar as alterações e gerar tabelas automaticamente.

2. Use **models** para estruturar os dados:
   - `User`: Para login e registro de usuários.
   - `Product`: Para armazenar os produtos.
   - `CartItem`: Para gerenciar itens do carrinho.
   - `Order`: Para registrar pedidos.

   - **Sugestão**: Inclua timestamps (`createdAt`, `updatedAt`) para rastrear alterações.

---

### **3. Criando Endpoints Básicos 🌐**
1. **Endpoints de autenticação**:
   - **POST `/auth/register`**: Crie novos usuários com hashing de senha usando `bcrypt`.
   - **POST `/auth/login`**: Retorne um token JWT após a validação.

   🔑 **Dica**: Armazene o segredo JWT em um arquivo `.env`:
   ```env
   JWT_SECRET=seu-segredo
   ```

2. **Endpoints de produtos**:
   - **GET `/products`**: Liste os produtos disponíveis.
   - **POST `/products`**: (Opcional para administradores) Adicione novos produtos ao catálogo.

3. **Endpoints do carrinho**:
   - **GET `/cart`**: Liste os itens do carrinho.
   - **POST `/cart`**: Adicione um produto ao carrinho.
   - **DELETE `/cart/:id`**: Remova um item.

   🛠 **Dica**: Use relacionamentos Sequelize para associar `CartItem` a `User` e `Product`.

---

### **4. Implementando Checkout e Pagamento 💳**
1. **Checkout protegido**:
   - Crie o middleware `authMiddleware` para validar o JWT:
     - Verifique o token no cabeçalho `Authorization`.
     - Retorne um erro 401 se o usuário não estiver autenticado.

2. **Simular pagamento**:
   - Crie a rota **POST `/checkout`**:
     - Simule o pagamento com um número aleatório de aprovação.
     - Retorne o status "Pagamento Aprovado" ou "Falha no Pagamento".

---

### **5. Simulando Entrega e Histórico de Pedidos 🚚**
1. **Simular entrega**:
   - **POST `/orders/:id/delivery`**:
     - Atualize o status do pedido para "Enviado".
     - Retorne a previsão de entrega.

2. **Histórico de pedidos**:
   - **GET `/orders/history`**:
     - Liste os pedidos do usuário logado.
     - Relacione `Order` com `User` para filtrar por cliente.

   📊 **Dica Extra**: Adicione um campo `status` ao modelo de pedido (`Order`) para acompanhar as etapas ("Pagamento Pendente", "Aprovado", "Enviado").

---

### **6. Melhorias e Funcionalidades Futuras 🔮**
1. **Adicionar categorias de produtos**:
   - Relacione os produtos a categorias e permita filtros no endpoint `/products`.

2. **Envio de notificações**:
   - Envie emails simulados no checkout utilizando a biblioteca `nodemailer`.

3. **Gerar relatórios de pedidos**:
   - Crie uma rota `/admin/reports` para gerar estatísticas de vendas.

4. **Documentação com Swagger**:
   - Use o **Swagger** para documentar suas APIs e facilitar o uso por outros desenvolvedores.

5. **Cache de produtos**:
   - Implemente caching com **Redis** para melhorar a performance do endpoint `/products`.

---

### **7. Testando e Deployando 🚀**
1. **Testes unitários**:
   - Use **Jest** para validar endpoints críticos como autenticação e checkout.

2. **Deploy**:
   - Faça o deploy com **Heroku** ou **Vercel**:
     ```bash
     heroku create coffee-shop-backend
     git push heroku main
     ```

3. **Monitore erros**:
   - Use ferramentas como **Sentry** para capturar erros no ambiente de produção.

---

### **8. Resultado Final 🎉**
Com esse backend, sua aplicação estará pronta para gerenciar:
- Registro e login de usuários 👤
- Produtos e carrinho de compras 🛒
- Pagamentos simulados 💳
- Histórico de pedidos e status de entrega 📦

✨ **Extra**: Adicione logs em todas as rotas para facilitar o debugging e crie um script de seed para popular o banco com produtos de teste!

Boa sorte no desenvolvimento! 🚀💻
