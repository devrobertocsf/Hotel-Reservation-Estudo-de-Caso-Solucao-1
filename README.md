# ⚠️ Hotel Reservation - Estudo de Caso: Solução 1 (Validação Manual na Camada de Aplicação)

Este repositório registra intencionalmente a **Solução 1** para o problema de validações de datas de reserva. Esta abordagem é didaticamente classificada como **muito ruim** por violar boas práticas de design de software e princípios da Programação Orientada a Objetos (POO).

## 🧐 Diagnóstico dos Problemas de Arquitetura

Embora o programa execute corretamente no terminal sob condições controladas, o código falha sob a perspectiva de Engenharia de Software nos seguintes pontos:

### 1. Quebra do Princípio de Responsabilidade Única (SRP)

A classe principal `Program.java` assumiu tarefas que não pertencem a ela. Ela precisa ler os dados do teclado, instanciar objetos e, cumulativamente, validar se a data de check-out é posterior ao check-in e se as atualizações contêm apenas datas futuras.

### 2. Entidade Anêmica (Sem Comportamento de Defesa)

A classe `Reservation.java` comporta-se meramente como uma estrutura de dados (*Anemic Domain Model*). Ela expõe métodos de alteração como o `updateDates` que realizam atribuições diretas sem checar a integridade do estado interno do objeto:

```java
public void updateDates(Date checkIn, Date checkOut) {
    this.checkIn = checkIn;
    this.checkOut = checkOut;
}

```

### 3. Código Espaguete e Duplicação de Lógica

Para gerenciar as possíveis falhas do usuário, o fluxo do programa descamba em estruturas condicionais encadeadas e repetitivas dentro do método `main`. Isso eleva a complexidade de manutenção e impede o reaproveitamento de código em outras partes do ecossistema do software.

## 📂 Estrutura de Arquivos Cadastrados

* `model.entities/Reservation.java`: Modelo anêmico contendo apenas os atributos, getters, setters, cálculo de diárias e o método de alteração sem validação.
* `application/Program.java`: Interface/Controlador acoplado acumulando todas as lógicas condicionais de validação de regras de negócio do domínio.

## 📉 Conclusão do Estudo

Este repositório serve como o "Ponto Zero" no aprendizado de manipulação de exceções. O objetivo de manter essa estrutura ruim salva é fixar o entendimento de que regras de negócio pertencem à própria entidade, preparando o terreno para a refatoração do sistema utilizando delegação e tratamentos defensivos com blocos `try-catch`.

## 📄 Licença

Este projeto de contraexemplo está sob a licença MIT.
