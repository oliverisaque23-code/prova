# prova 


Algoritmo "Auto_facil"
Var
   carro_modelo: vetor[1..100] de caractere
   carro_ano: vetor[1..100] de caractere
   carro_preco: vetor[1..100] de real
   n_carros, i, opcao: inteiro
   ano_atual: inteiro
   preco_temp: real

procedimento cadastrar_carro()
Inicio
   se n_carros >= 100 entao
      escreval("Limite máximo de carros atingido (100)!")
      retorne
   fimse

   n_carros <- n_carros + 1
   escreval("\nCadastro do ", n_carros, "º carro:")

   // Cadastro do modelo
   escreva("Modelo: ")
   leia(carro_modelo[n_carros])

   // Validação do ano (1990-2025)
   repita
      escreva("Ano (1990-", ano_atual, "): ")
      leia(carro_ano[n_carros])
      se (carro_ano[n_carros] < "1990") ou (carro_ano[n_carros] > "2025") entao
         escreval("Ano inválido! Digite entre 1990 e ", ano_atual, ".")
      fimse
   ate (carro_ano[n_carros] >= "1990") e (carro_ano[n_carros] <= "2025")

   // Validação do preço (mínimo R$10.000)
   repita
      escreva("Preço (mínimo R$10.000): R$")
      leia(preco_temp)
      se preco_temp < 10000 entao
         escreval("Valor inválido! Mínimo R$10.000")
      fimse
   ate preco_temp >= 10000

   carro_preco[n_carros] <- preco_temp
   escreval("Carro cadastrado com sucesso!")
fimprocedimento

procedimento listar_carros()
Inicio
   se n_carros = 0 entao
      escreval("\nNenhum carro cadastrado!")
   senao
      escreval("\n=== CARROS CADASTRADOS (", n_carros, ") ===")
      para i de 1 ate n_carros faca
         escreval(i, ". ", carro_modelo[i], " | Ano: ", carro_ano[i], " | Preço: R$", carro_preco[i])
      fimpara
      escreval("===============================")
   fimse
fimprocedimento

Inicio
   n_carros <- 0
   ano_atual <- 2025

   repita
      escreval("=== MENU AUTO FÁCIL ===")
      escreval("1. Cadastrar novo carro")
      escreval("2. Listar carros")
      escreval("0. Sair")
      escreva("Opção: ")
      leia(opcao)

      escolha opcao
      caso 1
         cadastrar_carro()
      caso 2
         listar_carros()
      caso 0
         escreval("Saindo do sistema...")
      outrocaso
         escreval("Opção inválida!")
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

   // Cadastro do email (validação simples)
   repita
      escreva("E-mail: ")
      leia(email[n_clientes])
      se nao contem("@", email[n_clientes]) ou nao contem(".", email[n_clientes]) entao
         escreval("E-mail inválido! Deve conter @ e .")
      fimse
   ate contem("@", email[n_clientes]) e contem(".", email[n_clientes])

   // Tipo de cliente
   repita
      escreva("Tipo (Física/Jurídica): ")
      leia(tipo_cliente[n_clientes])
      tipo_cliente[n_clientes] <- maiusc(tipo_cliente[n_clientes])
      se tipo_cliente[n_clientes] <> "FÍSICA" e tipo_cliente[n_clientes] <> "JURÍDICA" entao
         escreval("Digite 'Física' ou 'Jurídica'!")
      fimse
   ate tipo_cliente[n_clientes] = "FÍSICA" ou tipo_cliente[n_clientes] = "JURÍDICA"

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
