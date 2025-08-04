# prova 

Algoritmo "Auto_facil_simples"
Var
   carro_modelo: vetor[1..100] de caractere
   carro_ano: vetor[1..100] de inteiro
   carro_preco: vetor[1..100] de real
   carro_quantidade: vetor[1..100] de inteiro
   n_carros, i, opcao: inteiro
   preco_temp: real
   quantidade_temp: inteiro
   ano_atual: inteiro
   codigo, quantidade: inteiro
   total_pagar: real
   continuar: caractere

procedimento cadastrar_carro()
Inicio
   se n_carros >= 100 entao
      escreval("Limite máximo de carros atingido (100)!")
   senao
      n_carros <- n_carros + 1
      escreval("\nCadastro do ", n_carros, "º carro:")

      escreva("Modelo: ")
      leia(carro_modelo[n_carros])

      repita
         escreva("Ano (1990-", ano_atual, "): ")
         leia(carro_ano[n_carros])
         se (carro_ano[n_carros] < 1990) ou (carro_ano[n_carros] > ano_atual) entao
            escreval("Ano inválido! Digite entre 1990 e ", ano_atual, ".")
         fimse
      ate (carro_ano[n_carros] >= 1990) e (carro_ano[n_carros] <= ano_atual)

      repita
         escreva("Preço (mínimo R$10.000): R$")
         leia(preco_temp)
         se preco_temp < 10000 entao
            escreval("Valor inválido! Mínimo R$10.000")
         fimse
      ate preco_temp >= 10000

      carro_preco[n_carros] <- preco_temp

      repita
         escreva("Quantidade em estoque: ")
         leia(quantidade_temp)
         se quantidade_temp < 0 entao
            escreval("Quantidade inválida! Deve ser zero ou mais.")
         fimse
      ate quantidade_temp >= 0

      carro_quantidade[n_carros] <- quantidade_temp
      escreval("Carro cadastrado com sucesso!")
   fimse
fimprocedimento

procedimento listar_carros()
Inicio
   se n_carros = 0 entao
      escreval("\nNenhum carro cadastrado!")
   senao
      escreval("\n=== CARROS CADASTRADOS (", n_carros, ") ===")
      para i de 1 ate n_carros faca
         escreval(i, ". ", carro_modelo[i], " | Ano: ", carro_ano[i], " | Preço: R$", carro_preco[i]:0:2, " | Estoque: ", carro_quantidade[i])
      fimpara
      escreval("===============================")
   fimse
fimprocedimento

procedimento comprar_carro()
Inicio
   se n_carros = 0 entao
      escreval("\nNenhum carro disponível para venda!")
   senao
      listar_carros()
      escreval("\n=== COMPRAR CARRO ===")

      repita
         escreva("Digite o código do carro (0 para cancelar): ")
         leia(codigo)

         se codigo = 0 entao
            retorne
         fimse

         se (codigo < 1) ou (codigo > n_carros) entao
            escreval("Código inválido! Digite entre 1 e ", n_carros)
         senao
            repita
               escreva("Quantidade desejada (estoque: ", carro_quantidade[codigo], "): ")
               leia(quantidade)

               se quantidade <= 0 entao
                  escreval("Quantidade inválida!")
               senao se quantidade > carro_quantidade[codigo] entao
                  escreval("Quantidade indisponível em estoque!")
               senao
                  // Cálculos de preço
                  total_pagar <- carro_preco[codigo] * quantidade

                  // Desconto por quantidade (5% para +2 unidades)
                  se quantidade > 2 entao
                     total_pagar <- total_pagar * 0.95
                     escreval("Desconto de 5% aplicado (quantidade)")
                  fimse

                  // Desconto para carros antigos (10%)
                  se carro_ano[codigo] < ano_atual entao
                     total_pagar <- total_pagar * 0.90
                     escreval("Desconto de 10% aplicado (carro antigo)")
                  fimse

                  // Imposto de luxo (8% para compras >100.000)
                  se total_pagar > 100000 entao
                     total_pagar <- total_pagar * 1.08
                     escreval("Imposto de luxo de 8% aplicado")
                  fimse

                  // Confirmação da compra
                  escreval("\n=== RESUMO DA COMPRA ===")
                  escreval("Modelo: ", carro_modelo[codigo])
                  escreval("Ano: ", carro_ano[codigo])
                  escreval("Quantidade: ", quantidade)
                  escreval("Preço unitário: R$", carro_preco[codigo]:0:2)
                  escreval("TOTAL A PAGAR: R$", total_pagar:0:2)
                  escreval("=========================")

                  escreva("Confirmar compra? (S/N): ")
                  leia(continuar)

                  se (continuar = "S") ou (continuar = "s") entao
                     carro_quantidade[codigo] <- carro_quantidade[codigo] - quantidade
                     escreval("\nCompra realizada com sucesso!")
                     escreval("Novo estoque: ", carro_quantidade[codigo], " unidades")
                     interrompa
                  fimse
               fimse
            ate falso
         fimse
      ate falso
   fimse
fimprocedimento

Inicio
   n_carros <- 0
   ano_atual <- 2025

   repita
      escreval("\n=== MENU AUTO FÁCIL SIMPLES ===")
      escreval("1. Cadastrar novo carro")
      escreval("2. Listar carros")
      escreval("3. Comprar carro")
      escreval("0. Sair")
      escreva("Opção: ")
      leia(opcao)

      escolha opcao
      caso 1
         cadastrar_carro()
      caso 2
         listar_carros()
      caso 3
         comprar_carro()
      caso 0
         escreval("Saindo do sistema...")
      outrocaso
         escreval("Opção inválida! Digite entre 0 e 3")
      fimescolha
   ate opcao = 0
Fimalgoritmo






algoritmo "CadastroClientes"
var
   nome: vetor[1..100] de caractere
   telefone: vetor[1..100] de caractere
   email: vetor[1..100] de caractere
   endereco: vetor[1..100] de caractere
   codigo: vetor[1..100] de inteiro
   n_clientes, i, opcao: inteiro
   tipo_cliente: vetor[1..100] de caractere
   email_valido: logico
   pos_arroba, pos_ponto: inteiro
   qtde_arroba, j: inteiro
   parte_dominio: caractere
procedimento cadastrar_cliente()

inicio
   se n_clientes >= 100 entao
      escreval("Limite máximo de clientes atingido (100)!")
      retorne
   fimse

   n_clientes <- n_clientes + 1
   escreval("\nCadastro do ", n_clientes, "º cliente:")

   // Gera código automático (sequencial)
   codigo[n_clientes] <- 1000 + n_clientes
   escreval("Código gerado: ", codigo[n_clientes])

   // Cadastro do nome
   repita
      escreva("Nome completo: ")
      leia(nome[n_clientes])
      se compr(nome[n_clientes]) < 3 entao
         escreval("Nome deve ter pelo menos 3 caracteres!")
      fimse
   ate compr(nome[n_clientes]) >= 3

   // Cadastro do telefone
   repita
      escreva("Telefone (com DDD): ")
      leia(telefone[n_clientes])
      se compr(telefone[n_clientes]) < 8 entao
         escreval("Telefone inválido! Deve ter pelo menos 8 dígitos.")
      fimse
   ate compr(telefone[n_clientes]) >= 8

   // Cadastro do email (validação melhorada)
   repita
      escreva("E-mail: ")
      leia(email[n_clientes])

      email_valido <- verdadeiro
      qtde_arroba <- 0

      // Conta quantos @ tem no e-mail e guarda a posição
      para i de 1 ate compr(email[n_clientes]) faca
         se copia(email[n_clientes], i, 1) = "@" entao
            qtde_arroba <- qtde_arroba + 1
            pos_arroba <- i
         fimse
      fimpara

      // Verifica se tem exatamente um @
      se qtde_arroba <> 1 entao
         email_valido <- falso
      senao
         // Verifica se @ está no início ou final
         se (pos_arroba = 1) ou (pos_arroba = compr(email[n_clientes])) entao
            email_valido <- falso  // @ no começo ou final
         senao
            // Extrai o domínio (após @) para procurar o ponto
            parte_dominio <- copia(email[n_clientes], pos_arroba + 1, compr(email[n_clientes]) - pos_arroba)
            pos_ponto <- pos(".", parte_dominio)

            // Verifica se há ponto no domínio e sua posição
            se (pos_ponto = 0) ou (pos_ponto = compr(parte_dominio)) entao
               email_valido <- falso  // sem ponto ou ponto no final
            fimse
         fimse
      fimse

      se nao email_valido entao
         escreval("E-mail inválido! Formato correto: usuario@provedor.dominio")
      fimse
   ate email_valido
   // Tipo de cliente

   // Cadastro do endereço
   escreva("Endereço completo: ")
   leia(endereco[n_clientes])

   escreval("Cliente cadastrado com sucesso!")
fimprocedimento

procedimento listar_clientes()
inicio
   se n_clientes = 0 entao
      escreval("\nNenhum cliente cadastrado!")
   senao
      escreval("\n=== CLIENTES CADASTRADOS (", n_clientes, ") ===")
      escreval("CÓDIGO | NOME | TIPO | TELEFONE | E-MAIL")
      para i de 1 ate n_clientes faca
         escreval(codigo[i], " | ", nome[i], " | ", tipo_cliente[i], " | ", telefone[i], " | ", email[i])
      fimpara
      escreval("==============================================")
   fimse
fimprocedimento

procedimento buscar_cliente()
var
   cod_busca: inteiro
   encontrado: logico
inicio
   se n_clientes = 0 entao
      escreval("\nNenhum cliente cadastrado!")
      retorne
   fimse

   escreva("\nDigite o código para busca: ")
   leia(cod_busca)

   encontrado <- falso
   para i de 1 ate n_clientes faca
      se codigo[i] = cod_busca entao
         escreval("\nDADOS DO CLIENTE:")
         escreval("Código: ", codigo[i])
         escreval("Nome: ", nome[i])
         escreval("Tipo: ", tipo_cliente[i])
         escreval("Telefone: ", telefone[i])
         escreval("E-mail: ", email[i])
         escreval("Endereço: ", endereco[i])
         encontrado <- verdadeiro
         interrompa
      fimse
   fimpara

   se nao encontrado entao
      escreval("Cliente não encontrado!")
   fimse
fimprocedimento

inicio
   n_clientes <- 0

   repita
      escreval("\n=== SISTEMA DE CADASTRO DE CLIENTES ===")
      escreval("1. Cadastrar novo cliente")
      escreval("2. Listar todos os clientes")
      escreval("3. Buscar cliente por código")
      escreval("0. Sair")
      escreva("Opção: ")
      leia(opcao)

      escolha opcao
      caso 1
         cadastrar_cliente()
      caso 2
         listar_clientes()
      caso 3
         buscar_cliente()
      caso 0
         escreval("Encerrando o sistema...")
      outrocaso
         escreval("Opção inválida!")
      fimescolha
   ate opcao = 0
fimalgoritmo






