# 📧 Notificação — Microsserviço de Envio de E-mails

> 🎓 Projeto desenvolvido durante o curso da Javanauta Academy, com foco na construção de microsserviços independentes e comunicação entre serviços, incluindo envio de notificações por e-mail.

Microsserviço responsável pelo envio de notificações por **e-mail** para os usuários da plataforma **Agendador de Tarefas**. Utiliza **Spring Boot 4**, **Java 21**, **Spring Mail** e templates HTML renderizados com **Thymeleaf**.

---

## 🚀 Tecnologias

| Tecnologia | Versão |
|---|---|
| Java | 21 |
| Spring Boot | 4.0.3 |
| Spring Mail (JavaMailSender) | — |
| Thymeleaf (templates HTML) | — |
| Spring Web MVC | — |
| Lombok | — |
| Docker | — |
| Gradle | — |

---

## 📁 Estrutura do Projeto

```
notificacao/
├── .github/workflows/        # Pipelines CI/CD (GitHub Actions)
├── gradle/wrapper/           # Wrapper do Gradle
├── src/
│   ├── main/
│   │   ├── java/             # Controllers, Services e lógica de envio de e-mail
│   │   └── resources/
│   │       └── templates/    # Templates HTML (Thymeleaf) para os e-mails
│   └── test/                 # Testes unitários e de integração
├── Dockerfile                # Imagem Docker da aplicação
├── build.gradle              # Dependências e configurações de build
└── settings.gradle           # Configurações do projeto Gradle
```

---

## ⚙️ Configuração e Execução

### Pré-requisitos

- Java 21+
- Credenciais de um servidor SMTP (ex: Gmail, SendGrid, Mailtrap)
- Docker (opcional)
- Gradle (ou use o wrapper `./gradlew`)

### Configuração do servidor de e-mail

No arquivo `application.properties` ou via variáveis de ambiente:

```properties
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=seu-email@gmail.com
spring.mail.password=sua-senha-de-app
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
```

> 💡 Para testes locais, recomenda-se usar o [Mailtrap](https://mailtrap.io/) como servidor SMTP falso.

### Executando localmente

```bash
# Clone o repositório
git clone https://github.com/gabriela-oliveiraa/notificacao.git
cd notificacao

# Build do projeto
./gradlew build

# Execução
./gradlew bootRun
```

### Executando com Docker

```bash
# Build da imagem
docker build -t notificacao .

# Execute com variáveis de e-mail configuradas
docker run -p 8080:8080 \
  -e SPRING_MAIL_HOST=smtp.gmail.com \
  -e SPRING_MAIL_USERNAME=seu-email@gmail.com \
  -e SPRING_MAIL_PASSWORD=sua-senha \
  notificacao
```

---

## 📨 Templates de E-mail

Os e-mails são renderizados com **Thymeleaf**, permitindo templates HTML dinâmicos e personalizados. Os templates ficam em `src/main/resources/templates/`.

Exemplo de uso de variável no template:

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<body>
  <h1>Olá, <span th:text="${nomeUsuario}">Usuário</span>!</h1>
  <p>Você tem uma tarefa agendada: <strong th:text="${nomeTarefa}">Tarefa</strong></p>
</body>
</html>
```

---

## 🔗 Integração com outros serviços

Este microsserviço é chamado pelo **BFF** ou pelo **agendador-tarefas** para disparar notificações em eventos como:

- Criação de nova tarefa
- Lembrete de tarefa próxima ao prazo
- Confirmação de cadastro de usuário

Posição na arquitetura:

```
bff-agendador-tarefas  →  notificacao (disparo de e-mails)
agendador-tarefas      →  notificacao (lembrete de tarefas)
```

---

## 🧪 Testes

```bash
./gradlew test
```

---

## 📄 Licença

Este projeto foi desenvolvido para fins de estudo e prática com microsserviços em Java/Spring Boot.
