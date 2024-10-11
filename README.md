<h1>Projeto de Autenticação com Next.js e NextAuth</h1>

<p>Este projeto é uma aplicação web construída com <strong>Next.js</strong> e <strong>NextAuth</strong>, que implementa autenticação usando o Facebook. O objetivo é permitir que os usuários façam login de maneira simples e segura, aproveitando os recursos do NextAuth para gerenciar sessões e autenticação.</p>

<h2>Pré-requisitos</h2>
<p>Antes de executar o projeto, você precisa ter os seguintes requisitos instalados em sua máquina:</p>
<ul>
    <li><a href="https://nodejs.org/">Node.js</a> (v14 ou superior)</li>
    <li><a href="https://git-scm.com/">Git</a> (opcional, para controle de versão)</li>
</ul>

<h2>Instalação</h2>
<ol>
    <li>Clone o repositório:
        <pre><code>git clone https://github.com/sucloudflare/nextauth-facebook/tree/main</code></pre>
    </li>
    <li>Navegue até o diretório do projeto:
        <pre><code>cd nextauth-facebook</code></pre>
    </li>
    <li>Instale as dependências:
        <pre><code>npm install</code></pre>
    </li>
    <li>Crie um arquivo <code>.env.local</code> na raiz do projeto e adicione as seguintes variáveis de ambiente:
        <pre><code>
NEXTAUTH_URL=http://localhost:3000
FACEBOOK_CLIENT_ID=seu_facebook_client_id
FACEBOOK_CLIENT_SECRET=seu_facebook_client_secret
NEXTAUTH_SECRET=sua_chave_secreta
        </code></pre>
        <p>Certifique-se de substituir <code>seu_facebook_client_id</code> e <code>seu_facebook_client_secret</code> pelos valores obtidos ao registrar sua aplicação no <a href="https://developers.facebook.com/">Facebook Developer</a>.</p>
    </li>
</ol>

<h2>Executando o Projeto</h2>
<p>Para iniciar o servidor de desenvolvimento, execute:</p>
<pre><code>npm run dev</code></pre>
<p>A aplicação estará disponível em <a href="http://localhost:3000">http://localhost:3000</a>.</p>

<h2>Estrutura do Projeto</h2>
<ul>
    <li><strong>pages/</strong>
        <ul>
            <li><code>index.js</code>: Página inicial da aplicação.</li>
            <li><code>login.js</code>: Página de login usando NextAuth.</li>
        </ul>
    </li>
    <li><strong>api/</strong>
        <ul>
            <li><code>auth/[...nextauth].js</code>: Configuração do NextAuth para gerenciar a autenticação.</li>
        </ul>
    </li>
</ul>

<h2>Usando o NextAuth</h2>

<h3>O que é NextAuth?</h3>
<p><a href="https://next-auth.js.org/">NextAuth</a> é uma biblioteca de autenticação para aplicações Next.js que fornece uma maneira simples e segura de adicionar autenticação a suas aplicações. Com o NextAuth, você pode autenticar usuários usando provedores como Google, Facebook, Twitter, e outros.</p>

<h3>Configuração do NextAuth</h3>
<ol>
    <li><strong>Instalação</strong>: Primeiro, você deve instalar o NextAuth:
        <pre><code>npm install next-auth</code></pre>
    </li>
    <li><strong>Configuração do Provedor</strong>: No arquivo <code>api/auth/[...nextauth].js</code>, você pode configurar os provedores que deseja usar. Para autenticação com o Facebook, a configuração básica é assim:
        <pre><code>
import NextAuth from "next-auth";
import FacebookProvider from "next-auth/providers/facebook";

export default NextAuth({
  providers: [
    FacebookProvider({
      clientId: process.env.FACEBOOK_CLIENT_ID,
      clientSecret: process.env.FACEBOOK_CLIENT_SECRET,
    }),
  ],
  secret: process.env.NEXTAUTH_SECRET,
});
        </code></pre>
    </li>
    <li><strong>Gerenciamento de Sessão</strong>: Você pode usar o hook <code>useSession</code> do NextAuth em qualquer componente React para obter informações sobre a sessão do usuário, como mostrado na página inicial:
        <pre><code>
import { useSession } from "next-auth/react";

const HomePage = () => {
  const { data: session } = useSession();

  return (
    <div>
      {session ? (
        <p>Olá, {session.user.name}! Você está logado.</p>
      ) : (
        <Link href="/login">Login</Link>
      )}
    </div>
  );
};
        </code></pre>
    </li>
</ol>

<h2>Conclusão</h2>
<p>Este projeto é uma base para implementar autenticação em aplicações Next.js usando NextAuth e Facebook. Você pode expandi-lo adicionando mais funcionalidades, como logout, proteção de rotas e gerenciamento de usuários.</p>
<p>Para mais informações sobre NextAuth, consulte a <a href="https://next-auth.js.org/getting-started/introduction">documentação oficial</a>.</p>

<h2>Contribuição</h2>
<p>Sinta-se à vontade para contribuir com este projeto. Se você encontrar um erro ou tiver sugestões, abra uma issue ou um pull request.</p>

<h2>Licença</h2>
<p>Este projeto é licenciado sob a MIT License.</p>
